
# Example : BankX - Reasonable Requirements

- Transfers needs to be fast
- Payments Should be reliable
- Should be easy to extend in the future
- System must survive failures

# Questions
- Fast for whom? How to measure it? How fast is fast? 
- Reliable in what sense? 
- What counts as fast or successful payment?
- Which failures must the system survive?

## Exercise: 
- Identify three incompatible interpretations of "payment succeeded."


---

# Dictionary

- SLI (Service Level Indicator) 
- SLO (Service Level Objective)
- SLA (Service Level Agreement)

---


# Start with the Business / User Journey

**"Transfer journey"**:
- Submit → Validate → Accept → Book → Settle → Notify
- Login, choose recipient, choose account, amount ...


## Different promises
- "We received your request."
- "Your money has moved."
- "The transfer has settled."


## Distinguishing questions
- Which outcome is business-critical?
- Which steps does BankX control?
- Can a declined transfer be a correctly handled request?

**Exercise**: Mark critical outcomes and irreversible transitions.


---

# Define the Observation Boundary

- Possible measurements
  - API response time
  - Durable acceptance in the database
  - Final ledger state
  - External settlement confirmation

## Problem
- Fast `202 Accepted` ≠ durable acceptance
- Durable acceptance ≠ completed payment

# Decisions
- Start <---> end events
- System boundary and ownership
- User-visible meaning of each state


**Exercise**: Draw two different measurement intervals.

---


# Turn Requirements into SLIs

### SLI A — Durable acceptance
- Numerator: Eligible transfers durably accepted within 2 seconds
- Denominator: All eligible, valid transfer submissions

### SLI B — Timely finality
- Numerator: Transfers reaching posted / rejected within 60 seconds
- Denominator: All accepted transfers

### Edge cases
- Client retries and duplicate requests
- Timeouts and missing responses
- Valid business rejections vs technical failures
- Permanently stuck pending transfers

**Exercise**: Find two ways these metrics could give misleading results.

--- 

# Define Proper SLOs

**Acceptance SLO**
- ≥99.9% of eligible valid production transfers
- Durably accepted within 2 seconds
- Measured from public API ingress
- Rolling 30-day window

**Finality SLO**
- ≥99% of accepted production transfers
- Definitive outcome within 60 seconds
- Measured from durable acceptance
- Rolling 30-day window

**Error budgets**
- Acceptance: 0.1%
- Finality: 1%

**Questions**
- Who owns each SLO?
- Can external providers support these targets?
- What happens when error budgets are exhausted?

---

# Introduce a Failure Scenario

- **Incident**
  - External clearing provider p99 latency → 45 seconds
  - 3% of requests return 503 for 10 minutes
  - Clients retry timed-out requests
  - Notification service unavailable for 20 minutes

- **Constraints**
  - No acknowledged transfer may disappear
  - No duplicate posting
  - Customers must see truthful payment status

- **Challenge**
  - Which SLO breaches first?
  - Which dependencies create correlated failures?
  - What can BankX guarantee independently?

---

# Competing Architectural Solutions

A. Synchronous orchestration
 - API waits for ledger and clearing provider
 - Simple execution and state flow
 - Provider failures directly affect response latency


B. Queue and acknowledge
- Asynchronous processing
- Fast API response
- Risk of false acknowledgment without durable enqueue
- Requires backlog and retry management

C. Durable intent + outbox + workers

- Persist transfer intent before acknowledgment
- Transactional outbox and idempotent consumers
- Explicit status transitions and reconciliation
- Increased operational complexity

---

# Force the Architectural Trade-offs

- **Compare alternatives against**
  - API latency during provider slowness
  - Durability after acknowledgment
  - Duplicate prevention
  - Finality during external outages
  - Operational and recovery complexity

- **Discriminating questions**
  - Is accepted a durable promise?
  - Can payment status remain pending?
  - Can finality be separated from acceptance?
  - How much external dependency risk is acceptable?

- **Exercise**: Eliminate one architecture using a hard constraint, not preference.

---

# Make and Defend a Decision (ADR)
- Candidate: C — Durable intent + outbox + idempotent workers

Reasons
- Acceptance decoupled from clearing-provider latency
- Retries correlated to one logical transfer
- Deferred processing is visible and recoverable

Costs
- More states and infrastructure
- Reconciliation requirements
- Backlog management and observability

Unresolved conflict
- 60-second finality cannot be guaranteed through an unavailable provider

Architectural decision
- Improve provider redundancy or guarantees
- Renegotiate the business promise if necessary
- Do not hide provider failures through artificial metric exclusions


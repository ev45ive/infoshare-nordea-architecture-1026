# Architecture Exercise: The Payment That Wasn't Finished

Scenario: Three stakeholders

1. Product Owner — Conversion
- "Customers abandon transfers because confirmation takes too long."
- Reduce abandonment from 18% to 10% this quarter.
- Show customers confirmation within 2 seconds.
- No additional user steps.


2. Risk Officer — Correctness
- "We cannot tell customers their money was transferred when it wasn't."
- Never post the same transfer twice.
- Never exceed available funds without authorized credit.
- Every accepted transfer must be traceable and reconcilable.


3. Operations Lead — Reliability & Cost
- "The external clearing provider sometimes takes 8 seconds."
- Some requests time out with unknown outcomes.
- No budget for a second clearing provider.
- Keep processing cost below €0.10 per transfer.


System:
One transfer workflow: Submit → Validate → Post → Clear → Notify.

## Identify real drivers

Task
- Identify conflicting requirements.
- Ask which words conceal different assumptions.

## What is meaning of word "Confirmation" - Resolve ambiguities

- Request is revieved? UI interface status
- Durably accepted? - saved in db?
- Money posted? 
- External clearing confiremd?

- 2 second confirmation <> 8 seconds clearing.

> Stakeholder define success diferently


# Define business outcomes and metrics

- Product: "abandonment" 18% → 10%.
- Operations: €0.10/transfer. "cost"


**Task**
- Define one measurable business KPI for each stakeholder.
- Distinguish controllable system behavior from business outcomes.

# Extract functional requirements and invariants

New question
- "What must remain correct even if we miss performance targets?"

**Task**
- Define two non-negotiable invariants.
- Define the meaning of transfer states.


Invariant 1: One transfer causes at most one ledger debit
Invariant 2: Completed - authoritative evidence of success

## State: 
    Recieved -> Accepted -> Pending -> Completed (T)
             -> Rejected (T)        -> Failed (T)

> Define how funds are reserved or released on failure?

# Convert quality expectations into SLOs

- Product still demands a response in 2 seconds.
- Risk refuses misleading success messages.

**Task**:
- Define two SLIs and corresponding SLOs.
- Specify numerator, denominator, boundary and measurement window.

SLI:
- Eligible requests receiving a valid, durable acceptance or business rejection within 2 s ÷ all eligible requests

- Accepted transfers reaching a definitive outcome within 60s  ÷ all accepted transfer

SLO:
- ≥99.9%, rolling 30 days
- ≥98%, rolling 30 days



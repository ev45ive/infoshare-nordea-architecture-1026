
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


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
# Business & Functional Requirements

The same measurement and verification approach used for system quality attributes can be applied to business goals,
business processes, functional requirements, domain rules and invariants.

But not everything should become an SLO.

# Which mechanism measures what?

| Mechanism                 | Purpose                                                | BankX example                                                                       |
| ------------------------- | ------------------------------------------------------ | ----------------------------------------------------------------------------------- |
| Business KPI              | Measure business outcomes                              | 68% of customers complete onboarding                                                |
| Business metric           | Observe business behavior                              | 1,200 transfers submitted per hour                                                  |
| Business SLI              | Measure quality of a business service                  | 97% of accepted transfers finalized within 60 seconds                               |
| Business-process SLO      | Set a measurable service target                        | ≥99% finalized within 60 seconds                                                    |
| OKR / Business objective  | Define a desired business change                       | Increase onboarding conversion from 60% to 75% this quarter                         |
| Acceptance criteria       | Specify required functional behavior                   | Insufficient funds must cause a transfer rejection                                  |
| Domain invariant          | Express a rule that must always hold                   | No ledger transaction may become unbalanced                                         |
| Business fitness function | Verify that required business behavior remains correct | Replay transfers with retries and failures; verify exactly one valid ledger posting |
| Business alert            | Detect actionable deviations                           | Unresolved accepted transfers exceed permitted age                                  |


Goodhart's Law: “When a measure becomes a target, it ceases to be a good measure”

## Three different questions:
- Are we achieving the business goal? → KPIs / OKRs
- Are we delivering the promised business service? → SLIs / SLOs
- Is the system implementing the business rules correctly? → Acceptance tests / invariants / fitness functions

https://martinfowler.com/articles/domain-oriented-observability.html?utm_source=chatgpt.com


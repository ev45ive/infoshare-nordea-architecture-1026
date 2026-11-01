# Decision Tree

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evaluation & Decision Support".

Represents decisions, branching conditions, possible outcomes, and consequences, showing which architectural option fits under different constraints.

## Example 1: Simple - Database choice

```mermaid
flowchart TD
    Q1{"Strong consistency needed for ledger writes?"}
    Q1 -- Yes --> Q2{"Writes in more than one region?"}
    Q1 -- No --> Q3{"Records are document shaped?"}
    Q2 -- Yes --> A1["Distributed SQL cluster"]
    Q2 -- No --> A2["Relational database with read replicas"]
    Q3 -- Yes --> A3["Document store"]
    Q3 -- No --> A4["Key-value store"]
```

## Example 2: Realistic - Hosting by data residency

```mermaid
flowchart TD
    S["New workload with customer personal data"] --> R{"Must data stay in EU?"}
    R -- No --> C1["Public cloud, any region"]
    R -- Yes --> P{"Regulator requires on-premise?"}
    P -- Yes --> C2["Nordea on-premise data center"]
    P -- No --> K{"Customer-managed keys available?"}
    K -- Yes --> C3["Cloud EU region with customer-managed keys"]
    K -- No --> C4["Escalate to security architecture board"]
```

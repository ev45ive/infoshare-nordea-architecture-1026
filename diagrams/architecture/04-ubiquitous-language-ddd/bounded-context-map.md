# Bounded Context Map (DDD)

Mermaid type: `flowchart` (Approximate fit). Source: Modeling-Diagraming.md, section "Pipe, Pipe, pipe ... - Shared, Ubiqitous Language - Busines <> Code".

Shows bounded contexts and relationships such as Customer-Supplier, Shared Kernel, or Anti-Corruption Layer, answering where model boundaries should exist and which teams or systems must translate concepts between contexts.

## Example 1: Simple - Sales and Billing

```mermaid
flowchart LR
    subgraph Sales["Sales context"]
        Order["Order"]
    end
    subgraph Billing["Billing context"]
        Invoice["Invoice"]
    end
    Sales -- "Customer-Supplier" --> Billing
```

## Example 2: Realistic - Payments with shared kernel and legacy core

```mermaid
flowchart LR
    subgraph Pay["Payments context"]
        Authz["Authorization"]
    end
    subgraph Cards["Card processing context"]
        Scheme["Scheme gateway"]
    end
    subgraph Kernel["Shared kernel"]
        Money["Money, Currency"]
    end
    subgraph Core["Core banking (legacy)"]
        Ledger["Ledger"]
    end
    Pay -- "Shared Kernel" --- Kernel
    Cards -- "Customer-Supplier" --> Pay
    Pay -- "Anti-Corruption Layer" --> Core
```

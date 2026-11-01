# CQRS Read/Write Architecture Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Integration, APIs & Distributed Systems".

Separates commands, authoritative write models, projections, and query models, showing where state changes and where eventual consistency can arise.

## Example 1: Simple - Account ledger with a balance read model

```mermaid
flowchart LR
    subgraph Write["Write side (authoritative)"]
        Cmd["Transfer command handler"] --> Ledger[("Ledger event store")]
    end
    subgraph Read["Read side (query models)"]
        Proj["Balance projection"] --> RM[("Balance read model")]
    end
    App["Mobile app"] -- "TransferMoney command" --> Cmd
    App -- "GetBalance query" --> RM
    Ledger -- "AccountDebited, AccountCredited" --> Proj
```

## Example 2: Realistic - Payments with outbox and eventual consistency lag

```mermaid
flowchart LR
    subgraph Commands["Command side"]
        PayAPI["Payments API"] --> PayAgg["Payment aggregate, optimistic lock"]
        PayAgg --> PayDB[("Payments write DB")]
    end
    subgraph Projections["Projection pipeline"]
        Relay["Outbox relay (CDC)"] --> Bus[["Event stream"]]
        Bus --> ProjSearch["Search projector"]
        Bus -- "eventual, lag under 2 s" --> ProjStatus["Status projector"]
    end
    subgraph Queries["Query side"]
        Search[("Search index")]
        StatusDB[("Status read store")]
        Portal["Customer portal"]
    end
    PayDB -- "outbox row" --> Relay
    ProjSearch --> Search
    ProjStatus --> StatusDB
    Portal -- "GET payment status" --> StatusDB
    Portal -- "search" --> Search
```

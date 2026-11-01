# Distributed Consistency / Replication Diagram

Mermaid type: `sequenceDiagram` (Close fit). Source: Modeling-Diagraming.md, section "Integration, APIs & Distributed Systems".

Shows leaders, replicas, synchronization, quorum, and consistency relationships, including what happens during network partitions or concurrent updates.

## Example 1: Simple - Leader write replicated to two followers

```mermaid
sequenceDiagram
    autonumber
    participant C as Ledger client
    participant L as Leader
    participant F1 as Follower A, same region
    participant F2 as Follower B, DR region
    C->>L: Debit 100 EUR from account 123
    par Replicate to followers
        L->>F1: Append log entry 42
        F1-->>L: ACK
    and
        L->>F2: Append log entry 42
        F2-->>L: ACK
    end
    L-->>C: Committed, majority of 3 acknowledged
```

## Example 2: Realistic - Quorum read and write during a network partition

```mermaid
sequenceDiagram
    participant App as Payments service
    participant N1 as Node 1
    participant N2 as Node 2
    participant N3 as Node 3
    Note over N3: Network partition isolates Node 3
    App->>N1: Read balance for account 123, R=2
    N1->>N2: Read replica
    N2-->>N1: balance 500, version 7
    N1-->>App: balance 500, version 7, quorum of 2
    App->>N1: Debit 100, W=2
    N1->>N2: Replicate version 8
    N2-->>N1: ACK
    N1-->>App: Committed version 8
    Note over N3: Stale at version 7 until partition heals
```

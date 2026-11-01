# Saga / Distributed Transaction Diagram

Mermaid type: `sequenceDiagram` (Close fit). Source: Modeling-Diagraming.md, section "Distributed systems".

Shows distributed transaction steps, local commits, compensations, and failure paths.

## Example 1: Simple - Transfer across two ledgers with compensation
```mermaid
sequenceDiagram
    participant O as Transfer Orchestrator
    participant A as Ledger A (debit)
    participant B as Ledger B (credit)
    O->>A: Debit 500 EUR
    A-->>O: Committed
    O->>B: Credit 500 EUR
    B--xO: Timeout
    O->>A: Compensate: credit 500 EUR
    A-->>O: Compensated
    Note over O: Transfer marked FAILED
```

## Example 2: Realistic - Instant payment with reservation and release
```mermaid
sequenceDiagram
    autonumber
    participant C as Payment Channel
    participant P as Payment Orchestrator
    participant F as Fraud Service
    participant L as Core Ledger
    participant S as Instant Payment Scheme
    C->>P: Submit payment
    P->>F: Score payment
    F-->>P: Approved
    P->>L: Reserve funds (local commit)
    L-->>P: Reserved
    P->>S: Send credit transfer
    alt Scheme rejects or times out
        S-->>P: Rejected / timeout
        P->>L: Release reservation (compensate)
        L-->>P: Released
        P-->>C: Payment failed
    else Scheme accepts
        S-->>P: Accepted
        P->>L: Commit debit
        L-->>P: Committed
        P-->>C: Payment completed
    end
```

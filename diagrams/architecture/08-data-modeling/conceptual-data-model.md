# Conceptual Data Model

Mermaid type: `erDiagram` (Native fit). Source: Modeling-Diagraming.md, section "Data Architecture & Information Modeling".

Shows the high-level business information concepts and their relationships, independent of database technology, so stakeholders agree on what each term means.

## Example 1: Simple - customer, product, contract
```mermaid
erDiagram
    CUSTOMER ||--o{ CONTRACT : "signs"
    PRODUCT ||--o{ CONTRACT : "is described by"
    CONTRACT }o--|| ACCOUNT : "governs"
    CUSTOMER }o--o{ ADDRESS : "is reachable at"
```

## Example 2: Realistic - party roles in payments
```mermaid
erDiagram
    PARTY ||--o{ PAYER : "acts as"
    PARTY ||--o{ PAYEE : "acts as"
    PAYER }o--|| PAYMENT_ORDER : "initiates"
    PAYEE }o--|| PAYMENT_ORDER : "receives"
    PAYMENT_ORDER ||--o{ PAYMENT_EXECUTION : "is executed as"
    PAYMENT_EXECUTION }o--|| PAYMENT_SCHEME : "uses"
    PAYMENT_EXECUTION ||--o| SETTLEMENT : "results in"
```

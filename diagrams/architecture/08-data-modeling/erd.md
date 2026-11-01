# Entity-Relationship Diagram (ERD)

Mermaid type: `erDiagram` (Native fit). Source: Modeling-Diagraming.md, section "Data Architecture & Information Modeling".

Shows which entities exist, how they relate, and which identifiers and integrity constraints must hold.

## Example 1: Simple - customer, account, transaction
```mermaid
erDiagram
    CUSTOMER ||--o{ ACCOUNT : "holds"
    ACCOUNT ||--o{ TRANSACTION : "records"
    CUSTOMER {
        string customer_id PK
        string full_name
        date date_of_birth
    }
    ACCOUNT {
        string account_id PK
        string customer_id FK
        string iban UK
        string currency
    }
    TRANSACTION {
        string transaction_id PK
        string account_id FK
        decimal amount
        timestamp booked_at
    }
```

## Example 2: Realistic - card authorization and settlement
```mermaid
erDiagram
    ACCOUNT ||--o{ CARD : "linked to"
    CARD ||--o{ CARD_AUTHORIZATION : "used in"
    MERCHANT ||--o{ CARD_AUTHORIZATION : "accepts"
    CARD_AUTHORIZATION ||--o| SETTLEMENT : "settled by"
    CARD {
        string card_id PK
        string account_id FK
        string masked_pan
    }
    MERCHANT {
        string merchant_id PK
        string merchant_category_code
    }
    CARD_AUTHORIZATION {
        string authorization_id PK
        string card_id FK
        string merchant_id FK
        decimal amount
        string decision
    }
    SETTLEMENT {
        string settlement_id PK
        string authorization_id FK
        date settlement_date
    }
```

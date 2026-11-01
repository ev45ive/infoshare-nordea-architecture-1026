# Physical Data Model

Mermaid type: `erDiagram` (Native fit). Source: Modeling-Diagraming.md, section "Data Architecture & Information Modeling".

Shows the concrete tables, column types, keys, and storage details that will be implemented in the database.

## Example 1: Simple - accounts and account transactions
```mermaid
erDiagram
    ACCOUNTS ||--o{ ACCOUNT_TRANSACTIONS : "posts"
    ACCOUNTS {
        bigint account_id PK "identity column"
        varchar iban UK "ISO 13616, max 34 chars"
        char currency "ISO 4217, NOT NULL"
        numeric balance "precision 18, scale 2, NOT NULL, default 0"
        varchar status "ACTIVE, FROZEN or CLOSED"
        timestamp created_at "NOT NULL, audit"
        varchar created_by "NOT NULL, audit"
    }
    ACCOUNT_TRANSACTIONS {
        bigint transaction_id PK "identity column"
        bigint account_id FK "indexed"
        numeric amount "precision 18, scale 2, NOT NULL"
        char currency "ISO 4217"
        date value_date "NOT NULL"
        timestamp created_at "NOT NULL, audit"
    }
```

## Example 2: Realistic - partitioned ledger entries
```mermaid
erDiagram
    ACCOUNTS ||--o{ LEDGER_ENTRIES : "has"
    LEDGER_ENTRIES }o--|| TRANSACTION_TYPES : "classified by"
    LEDGER_ENTRIES {
        bigint entry_id PK "identity column"
        bigint account_id FK "indexed"
        varchar type_code FK
        numeric amount "precision 18, scale 2, NOT NULL"
        char currency "ISO 4217"
        date value_date "range partition key"
        varchar external_reference "unique per account, indexed"
        timestamp created_at "NOT NULL, audit"
    }
    TRANSACTION_TYPES {
        varchar type_code PK
        varchar description
    }
```

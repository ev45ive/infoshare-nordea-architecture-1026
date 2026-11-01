# Logical Data Model

Mermaid type: `erDiagram` (Native fit). Source: Modeling-Diagraming.md, section "Data Architecture & Information Modeling".

Shows data structures, keys, relationships, and cardinalities in normalized form, without tying them to a specific DBMS.

## Example 1: Simple - customer, address, and bridge table
```mermaid
erDiagram
    CUSTOMER ||--o{ CUSTOMER_ADDRESS : "has"
    ADDRESS ||--o{ CUSTOMER_ADDRESS : "is used as"
    CUSTOMER {
        string customer_id PK
        string national_id UK
        date date_of_birth
    }
    ADDRESS {
        string address_id PK
        string street_line
        string postal_code
        string country_code
    }
    CUSTOMER_ADDRESS {
        string customer_id PK, FK
        string address_id PK, FK
        string address_type PK
        date valid_from
    }
```

## Example 2: Realistic - customer product holdings
```mermaid
erDiagram
    CUSTOMER ||--o{ PRODUCT_HOLDING : "holds"
    PRODUCT ||--o{ PRODUCT_HOLDING : "is held as"
    CUSTOMER {
        string customer_id PK
        string kyc_status
    }
    PRODUCT {
        string product_id PK
        string product_type
    }
    PRODUCT_HOLDING {
        string customer_id PK, FK
        string product_id PK, FK
        date opened_on
        string holding_status
    }
```

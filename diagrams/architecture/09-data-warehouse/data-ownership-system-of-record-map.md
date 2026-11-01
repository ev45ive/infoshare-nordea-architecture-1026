# Data Ownership / System-of-Record Map

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Data warehouse".

It answers which system owns each piece of data, who may update it, and where conflicting sources of truth exist.

## Example 1: Simple - customer master owned by CRM
```mermaid
flowchart LR
    subgraph CRM["CRM domain (owner)"]
        CUST[("Customer master")]
    end
    subgraph Onboarding["Onboarding domain"]
        KYC[("KYC records")]
    end
    subgraph Cards["Cards domain"]
        CARDAPP["Card application"]
    end
    CUST -->|"read-only copy"| CARDAPP
    KYC -.->|"address (conflicts with CRM)"| CUST
    CUST -->|"read-only"| DWH[("Enterprise data warehouse")]
```

## Example 2: Realistic - balance, price and payment status ownership
```mermaid
flowchart LR
    subgraph Core["Core banking (SoR: balance, IBAN)"]
        CORE[("Core ledger")]
    end
    subgraph Pricing["Pricing team (SoR: product catalog)"]
        PCAT[("Product catalog")]
    end
    subgraph Payments["Payments (SoR: payment status)"]
        PAY[("Payment hub")]
    end
    subgraph Analytics["Data platform (copies only)"]
        DWH[("Warehouse")]
    end
    PCAT -->|"publishes price"| CORE
    PAY -->|"writes status"| CORE
    CORE -->|"CDC replica"| DWH
    PCAT -->|"CDC replica"| DWH
    PAY -.->|"status conflicts with core"| DWH
```

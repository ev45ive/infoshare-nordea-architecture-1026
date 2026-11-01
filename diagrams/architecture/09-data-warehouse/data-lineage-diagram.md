# Data Lineage Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Data warehouse".

It answers where data came from and which downstream reports, models, or services are affected if a source changes.

## Example 1: Simple - core banking to risk report
```mermaid
flowchart LR
    CB[("Core banking<br/>accounts")] -->|"nightly extract"| STG[("Staging<br/>stg_accounts")]
    STG -->|"net exposure calc"| DM[("Risk data mart<br/>exposure_daily")]
    DM -->|"aggregate by segment"| RPT["Regulatory credit risk report"]
```

## Example 2: Realistic - card transaction field lineage
```mermaid
flowchart LR
    subgraph Sources
        CARDS[("Card processor<br/>txn_amount_minor")]
        LEDGER[("General ledger<br/>GL postings")]
    end
    subgraph Warehouse
        STG[("stg_card_txn")]
        CONF["Conform amount to EUR"]
        FACT[("fact_card_txn")]
    end
    CARDS --> STG --> CONF --> FACT
    LEDGER --> FACT
    FACT --> LIQ["Liquidity model"]
    FACT --> COREP["COREP return"]
```

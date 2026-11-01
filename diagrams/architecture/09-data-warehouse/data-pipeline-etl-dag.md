# Data Pipeline / ETL DAG

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Data warehouse".

It answers in what order datasets must be processed, what happens if a transformation fails, and which stages can run in parallel.

## Example 1: Simple - nightly card transaction load
```mermaid
flowchart LR
    EXT1["Extract card txns"] --> STG[("Stage raw")]
    EXT2["Extract GL postings"] --> STG
    STG --> VAL{"Row count and checksum"}
    VAL -->|pass| TRF["Transform and conform"]
    VAL -->|fail| ALERT["Quarantine, alert on-call"]
    TRF --> LOAD[("fact_card_txn")]
```

## Example 2: Realistic - parallel extracts merged for regulatory feed
```mermaid
flowchart LR
    subgraph Extract["Parallel extracts"]
        E1["Core accounts"]
        E2["Card txns"]
        E3["Customer KYC"]
    end
    E1 --> T1["Transform accounts"]
    E2 --> T2["Transform txns"]
    E3 --> T3["Mask PII"]
    T1 & T2 & T3 --> DQ{"DQ checks"}
    DQ -->|pass| L1[("dim_account")]
    DQ -->|pass| L2[("fact_txn")]
    DQ -->|fail| HOLD["Hold load, notify steward"]
    L1 --> RPT["COREP feed"]
    L2 --> RPT
```

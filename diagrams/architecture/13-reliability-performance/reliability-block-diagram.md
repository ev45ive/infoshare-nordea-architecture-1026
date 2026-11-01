# Reliability Block Diagram (RBD)

Mermaid type: `flowchart` LR with parallel branches (Approximate fit). Source: Modeling-Diagraming.md, section "Reliability, Performance & Quality Attributes".

Models series, parallel, and redundant dependencies so that component reliabilities can be combined and the availability gain from redundancy can be judged.

## Example 1: Simple - redundant app servers in front of a database

```mermaid
flowchart LR
    CL["Client"] --> LB["Load balancer R=0.999"]
    LB --> A1["App server A R=0.99"] & A2["App server B R=0.99"]
    A1 & A2 --> DB["Database primary R=0.995"]
```

## Example 2: Realistic - card authorization path

```mermaid
flowchart LR
    NET["Card network"] --> ING1["Ingress zone 1 R=0.999"] & ING2["Ingress zone 2 R=0.999"]
    ING1 & ING2 --> GW1["Auth gateway pod 1 R=0.98"] & GW2["Auth gateway pod 2 R=0.98"] & GW3["Auth gateway pod 3 R=0.98"]
    GW1 & GW2 & GW3 --> DB1["Ledger DB primary R=0.995"] & DB2["Ledger DB standby R=0.995"]
    DB1 & DB2 --> CORE["Core ledger R=0.999"]
```

# High-Availability / Multi-Region Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Infrastructure, Deployment & Network Architecture".

Shows redundant components, availability zones, regions, failover paths, and replication relationships.

## Example 1: Simple - active-passive region failover

```mermaid
flowchart TB
    dns{{Global DNS with health checks}}
    subgraph R1 ["Region A (primary)"]
        lb1[Load Balancer]
        app1[Payments API]
        db1[(Primary DB)]
        lb1 --> app1 --> db1
    end
    subgraph R2 ["Region B (standby)"]
        lb2[Load Balancer]
        app2[Payments API]
        db2[(Standby DB)]
        lb2 --> app2 --> db2
    end
    dns -->|active| lb1
    dns -.->|failover only| lb2
    db1 ==>|sync replication| db2
```

## Example 2: Realistic - ledger cluster across three zones with DR region

```mermaid
flowchart LR
    client([Clients]) --> gslb{{Global Traffic Manager}}
    subgraph R1 ["Region EU-North (active)"]
        subgraph Z1 ["Zone 1"]
            p1[(Ledger Primary)]
        end
        subgraph Z2 ["Zone 2"]
            s1[(Ledger Replica)]
        end
        subgraph Z3 ["Zone 3"]
            w1{{Quorum Witness}}
        end
        p1 ==>|sync| s1
        p1 -.->|vote| w1
    end
    subgraph R2 ["Region EU-West (DR)"]
        s2[(Ledger DR Replica)]
    end
    gslb --> p1
    p1 -.->|async| s2
```

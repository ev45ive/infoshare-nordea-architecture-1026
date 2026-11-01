# Environment / Release Topology

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Infrastructure, Deployment & Network Architecture".

Maps development, testing, staging, production, and their configuration or data dependencies.

## Example 1: Simple - promotion path with hotfix route

```mermaid
flowchart LR
    dev[Dev] --> test[Test]
    test --> staging[Staging]
    staging -->|change approval| prod[Production]
    hotfix[Hotfix branch] -.->|emergency path| prod
```

## Example 2: Realistic - promotion gates with per-environment configuration and data

```mermaid
flowchart LR
    subgraph DEV ["Dev (synthetic data)"]
        d1[Build and unit tests]
    end
    subgraph TST ["Test (masked data)"]
        t1[Integration and regression]
    end
    subgraph STG ["Staging (prod-like config)"]
        s1[Performance and security scan]
    end
    subgraph PRD ["Production (real data)"]
        p1[Canary then full rollout]
    end
    d1 --> t1 --> s1
    s1 -->|CAB approval| p1
    hf[Hotfix branch] -->|expedited CAB| p1
    cfg[(Per-environment config store)] -.-> t1
    cfg -.-> s1
    cfg -.-> p1
```

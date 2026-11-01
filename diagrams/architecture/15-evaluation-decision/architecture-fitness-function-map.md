# Architecture Fitness Function Map

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evaluation & Decision Support".

Connects architectural characteristics and constraints to automated or manual verification mechanisms, showing how architecture rules are checked continuously and which properties could silently regress.

## Example 1: Simple - Automated checks in CI

```mermaid
flowchart LR
    C1["No direct UI access to database"] --> M1["ArchUnit rule in CI"]
    C2["p95 payment latency under 300 ms"] --> M2["Nightly load test gate"]
    C3["PII never written to logs"] --> M3["Static scan on merge"]
    M1 --> G["Pipeline fails build"]
    M2 --> G
    M3 --> G
```

## Example 2: Realistic - Characteristics mapped to verification

```mermaid
flowchart LR
    subgraph Characteristics
        A["Ledger writes are idempotent"]
        B["Customer data stays in EU"]
        C["Modules depend only downward"]
    end
    subgraph Verification
        V1["Contract test on payment API in CI"]
        V2["Residency check in Terraform policy"]
        V3["ArchUnit rule in build"]
        V4["Quarterly architecture review"]
    end
    A --> V1
    B --> V2
    B -. "manual exception review" .-> V4
    C --> V3
```

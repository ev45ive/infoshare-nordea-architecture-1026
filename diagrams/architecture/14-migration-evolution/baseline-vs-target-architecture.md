# Baseline vs. Target Architecture Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evolution, Migration & Planning".

Compares the current architecture with the desired future structure, showing what must change, which limitations are removed, and which new dependencies are introduced.

## Example 1: Simple - Payments monolith to target services

```mermaid
flowchart LR
    subgraph Baseline["Baseline today"]
        B1[Monolithic payments engine]
        B2[(Shared Oracle ledger)]
        B1 --> B2
    end
    subgraph Target["Target state"]
        T1[Payment initiation API]
        T2[Payment routing service]
        T3[(Ledger service DB)]
        T4[Event bus]
        T1 --> T2
        T2 --> T4
        T4 --> T3
    end
    Baseline -. replaced by .-> Target
```

## Example 2: Realistic - Core banking decoupling

```mermaid
flowchart LR
    subgraph Baseline["Baseline 2026"]
        MOB1[Mobile app] --> CORE1[Core banking mainframe]
        TELL1[Branch teller UI] --> CORE1
        CRM1[CRM] -->|nightly batch file| CORE1
        REG1[Regulatory reporting] -->|direct SQL| CORE1
    end
    subgraph Target["Target 2028"]
        MOB2[Mobile app] --> GW[API gateway]
        TELL2[Branch teller UI] --> GW
        GW --> ACC[Account service]
        ACC --> LEDGER[Core ledger adapter]
        ACC --> EVT[(Account event stream)]
        EVT --> CRM2[CRM]
        EVT --> REG2[Regulatory data mart]
    end
```

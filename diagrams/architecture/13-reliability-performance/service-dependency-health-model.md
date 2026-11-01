# Service Dependency / Health Model

Mermaid type: `flowchart` with `classDef` health colors (Close fit). Source: Modeling-Diagraming.md, section "Reliability, Performance & Quality Attributes".

Maps services and dependencies with health signals and degradation states, showing which failures affect critical user journeys and SLOs.

## Example 1: Simple - checkout dependencies

```mermaid
flowchart TD
    CHK["Checkout"] --> PAY["Payments API"]
    CHK --> AUTH["Auth service"]
    CHK --> CAT["Product catalog"]
    classDef healthy fill:#c8e6c9,stroke:#2e7d32
    classDef degraded fill:#fff59d,stroke:#f9a825
    class PAY,AUTH healthy
    class CAT degraded
```

## Example 2: Realistic - mobile money transfer journey

```mermaid
flowchart LR
    APP["Mobile app: send money"] --> GW["API gateway"]
    GW --> ID["Identity service"]
    GW --> TX["Transfer service"]
    TX --> SCR["Sanctions screening"]
    TX --> CORE["Core banking adapter"]
    TX -.-> NOTIF["Notification service"]
    CORE --> ACC[("Account DB")]
    classDef healthy fill:#c8e6c9,stroke:#2e7d32
    classDef degraded fill:#fff59d,stroke:#f9a825
    classDef down fill:#ffcdd2,stroke:#c62828
    class APP,GW,ID,TX,CORE,ACC healthy
    class SCR degraded
    class NOTIF down
```

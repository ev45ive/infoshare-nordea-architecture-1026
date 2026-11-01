# Migration Dependency Graph

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evolution, Migration & Planning".

Shows technical, business, data, and organizational prerequisites between migration tasks, answering what must happen first, which tasks block other work, and where the critical path runs.

## Example 1: Simple - Go-live prerequisites

```mermaid
flowchart LR
    DM[Data migration of accounts] --> API[API cutover]
    SEC[Security review passed] --> API
    API --> GL[Go-live]
    REG[Regulator sign-off] --> GL
    TR[Operations staff trained] --> GL
```

## Example 2: Realistic - Card platform critical path

```mermaid
flowchart LR
    classDef critical fill:#fdd,stroke:#c00,stroke-width:2px
    CLEAN[Card data cleansing]:::critical --> VAULT[Token vault migration]:::critical
    VAULT --> TEST[Adapter integration tests]:::critical
    ADAPT[Issuer API adapter] --> TEST
    TEST --> CUT[Production cutover]:::critical
    PCI[PCI audit approval] --> CUT
    OPS[Operations runbook signed off] --> CUT
```

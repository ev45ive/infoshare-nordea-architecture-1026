# Transition Architecture Diagram (ArchiMate)

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evolution, Migration & Planning".

Represents intermediate architectural states between baseline and target, showing what must coexist during migration and which viable states the organization can operate in.

## Example 1: Simple - Card switch during split traffic

```mermaid
flowchart LR
    subgraph Baseline["Baseline Q1"]
        LEG1[Legacy card switch]
    end
    subgraph Transition["Transition Q2 to Q4"]
        BRIDGE[Anti-corruption bridge]
        LEG2[Legacy card switch]
        HUB[Cloud card hub]
        BRIDGE -->|low-risk BINs| HUB
        BRIDGE -->|remaining BINs| LEG2
    end
    subgraph Target["Target state"]
        HUB2[Cloud card hub]
    end
    LEG1 -.->|split traffic| BRIDGE
    HUB -.->|all traffic| HUB2
```

## Example 2: Realistic - CRM integration during dual running

```mermaid
flowchart TB
    subgraph Baseline["Baseline"]
        CRM1[Legacy CRM] -->|nightly file| DW1[(Data warehouse)]
    end
    subgraph Transition["Transition dual running"]
        CRM2[Legacy CRM] -->|nightly file| DW2[(Data warehouse)]
        CRM2 -->|CDC events| SYNC[Sync service]
        SYNC -->|reconciliation check| NEWCRM[Cloud CRM]
        SYNC -.->|mismatch alerts| OPS[Ops dashboard]
    end
    subgraph Target["Target state"]
        NEWCRM2[Cloud CRM] -->|CDC events| DW3[(Data warehouse)]
    end
```

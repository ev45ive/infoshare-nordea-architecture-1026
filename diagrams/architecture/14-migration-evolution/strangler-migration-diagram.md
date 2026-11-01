# Strangler Migration Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evolution, Migration & Planning".

Shows legacy and replacement systems coexisting while responsibilities are incrementally redirected, answering which capabilities can move independently, how traffic is switched, and when the legacy implementation can be retired.

## Example 1: Simple - Card endpoints behind a facade

```mermaid
flowchart LR
    APP[Mobile banking app] --> FAC{API facade}
    FAC -->|"/cards/block"| NEW[Card service]
    FAC -->|"/cards/limits"| NEW
    FAC -->|"/cards/statement"| OLD[Legacy card monolith]
    NEW --> DB1[(Cards DB)]
    OLD --> DB2[(Mainframe card file)]
```

## Example 2: Realistic - Savings accounts shifted by traffic share

```mermaid
flowchart TB
    subgraph Channels
        WEB[Internet banking]
        APP[Mobile app]
    end
    GW{API gateway<br/>traffic router}
    subgraph Legacy["Legacy core - to retire"]
        L1[Savings accounts]
        L2[Mortgages]
    end
    subgraph Replacement["New platform"]
        N1[Savings accounts]
        N2[Current accounts]
    end
    WEB --> GW
    APP --> GW
    GW -->|10 percent| L1
    GW -->|90 percent| N1
    GW --> L2
    GW --> N2
```

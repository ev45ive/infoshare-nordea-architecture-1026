# Integration Architecture Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Integration, APIs & Distributed Systems".

Maps systems, APIs, brokers, integration middleware, protocols, and connections, showing which integrations are synchronous, asynchronous, or batch-based.

## Example 1: Simple - Payments and core banking behind an API gateway

```mermaid
flowchart LR
    Mobile["Mobile banking app"]
    subgraph Nordea["Nordea internal"]
        GW["API gateway"] -- "REST, sync" --> Core["Core banking"]
        GW -- "gRPC, sync" --> Pay["Payments hub"]
        Core -- "Nightly SFTP file, batch" --> Reg["Regulatory reporting"]
    end
    Mobile -- "REST over HTTPS, sync" --> GW
    Pay -- "ISO 20022 over MQ, async" --> Clr["Clearing house"]
```

## Example 2: Realistic - Customer onboarding with ESB, event bus and batch reporting

```mermaid
flowchart LR
    subgraph Channels["Channels"]
        App["Onboarding app"]
    end
    subgraph Integration["Integration layer"]
        APIM["API management"]
        ESB["ESB mediation"]
        Kafka[("Kafka event bus")]
    end
    subgraph Systems["Core systems"]
        CRM["CRM"]
        Core["Core banking"]
        Risk["Credit scoring"]
    end
    App -- "REST, sync" --> APIM
    APIM -- "REST, sync" --> ESB
    ESB -- "SOAP, sync" --> Core
    APIM -- "REST, sync, timeout 2 s" --> Risk
    Core -- "AccountOpened, async" --> Kafka
    Kafka -- "Customer events, async" --> CRM
    Core -- "Daily flat file, batch" --> Reg["Regulatory reporting"]
```

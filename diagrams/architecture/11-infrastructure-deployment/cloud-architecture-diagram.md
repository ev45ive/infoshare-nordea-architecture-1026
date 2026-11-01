# Cloud Architecture Diagram

Mermaid type: `architecture-beta` (Close fit). Source: Modeling-Diagraming.md, section "Infrastructure, Deployment & Network Architecture".

Represents managed services, regions, accounts, subscriptions, storage, compute, and connectivity.

## Example 1: Simple - web app, CDN, API and managed database in one region

```mermaid
architecture-beta
    group region(cloud)[EU Cloud Region]
    service users(internet)[Customers]
    service cdn(internet)[CDN] in region
    service web(server)[Web App] in region
    service api(server)[Accounts API] in region
    service db(database)[Managed SQL DB] in region
    users:R --> L:cdn
    cdn:R --> L:web
    web:R --> L:api
    api:R --> L:db
```

## Example 2: Realistic - mobile payments on cloud services with reporting pipeline

```mermaid
architecture-beta
    group platform(cloud)[Cloud Platform EU]
    group dplat(cloud)[Data Platform]
    service mobile(internet)[Mobile App]
    service gw(server)[API Gateway] in platform
    service idp(server)[Auth Service] in platform
    service stream(disk)[Event Queue] in platform
    service ledger(database)[Ledger DB] in platform
    service lake(database)[Data Lake] in dplat
    service reg(server)[Regulatory Reporting] in dplat
    mobile:R --> L:gw
    gw:R --> L:idp
    idp:B --> T:ledger
    ledger:R --> L:stream
    stream:R --> L:lake
    lake:R --> L:reg
```

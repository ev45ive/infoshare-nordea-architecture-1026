# Layered Architecture Diagram

Mermaid type: `block-beta` (Close fit). Source: Modeling-Diagraming.md, section "Boundaries & Decomposition".

Source gives no description for this item. The diagram shows a system organized into stacked layers, from channels down to persistence and platform.

## Example 1: Simple - four stacked layers

```mermaid
block-beta
    columns 1
    presentation["Presentation: mobile app, internet banking, branch teller UI"]
    api["API layer: gateway, authentication, rate limiting"]
    domain["Domain services: payments, accounts, onboarding"]
    persistence["Persistence: core ledger, document store, event log"]
```

## Example 2: Realistic - channels, services, data, and platform

```mermaid
block-beta
    columns 3
    mobile["Mobile app"] web["Internet banking"] teller["Branch teller"]
    gateway["API gateway and BFF"]:3
    payments["Payments"] accounts["Accounts"] reporting["Regulatory reporting"]
    ledger["Core banking ledger"]:2 datastore["Operational data store"]
    platform["Platform: Kubernetes, Kafka, observability"]:3
```

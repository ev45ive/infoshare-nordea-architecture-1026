# Event-Driven Architecture Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Integration, APIs & Distributed Systems".

Maps event producers, brokers, topics, subscriptions, and consumers, showing where coupling is introduced and which delivery or ordering dependencies apply.

## Example 1: Simple - Payments and card events fanning out to consumers

```mermaid
flowchart LR
    subgraph Producers
        Pay["Payments service"]
        Cards["Card authorization"]
    end
    subgraph Broker["Event broker (Kafka)"]
        T1[["payments.settled"]]
        T2[["cards.authorized"]]
    end
    subgraph Consumers
        Ledger["General ledger"]
        Rep["Regulatory reporting"]
        Fraud["Fraud scoring"]
    end
    Pay -- "publish" --> T1
    Cards -- "publish" --> T2
    T1 -- "subscribe, ordered per account" --> Ledger
    T1 -- "subscribe" --> Rep
    T2 -- "subscribe" --> Fraud
```

## Example 2: Realistic - Account events with consumer groups and dead-letter handling

```mermaid
flowchart LR
    Core["Core banking"] -- "AccountUpdated, at-least-once" --> T1[["account.updated"]]
    T1 -- "consumer group: crm" --> CRM["CRM sync"]
    T1 -- "consumer group: reporting" --> DWH["Data warehouse loader"]
    T1 -- "consumer group: alerts" --> Alert["Fraud alert service"]
    Alert -- "FraudAlertRaised" --> T2[["fraud.alerts"]]
    T2 -- "subscribe" --> Case["Case management"]
    DWH -. "poison message" .-> DLQ[("account.updated.dlq")]
    Alert -. "poison message" .-> DLQ
```

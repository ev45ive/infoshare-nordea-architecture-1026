# System Context Diagram (C4 Level 1)

Mermaid type: `C4Context` (Native fit). Source: Modeling-Diagraming.md, section "System Context, Boundaries & Decomposition".

Shows one system in relation to its users, external systems, and integrations.

## Example 1: Simple - mobile banking

```mermaid
C4Context
    title Mobile banking - system context
    Person(customer, "Retail customer", "Uses the mobile app")
    System(mobile, "Mobile banking", "Nordea mobile app and API")
    System_Ext(core, "Core banking", "Accounts and ledger")
    System_Ext(payprov, "Payment provider", "Executes SEPA and card payments")
    Rel(customer, mobile, "Views accounts and pays")
    Rel(mobile, core, "Reads balances, posts transactions", "REST/JSON")
    Rel(mobile, payprov, "Initiates payments", "HTTPS")
```

## Example 2: Realistic - card fraud monitoring

```mermaid
C4Context
    title Card fraud monitoring - system context
    Person(analyst, "Fraud analyst", "Reviews flagged transactions")
    System(fraud, "Fraud monitoring", "Scores card transactions in real time")
    System_Ext(scheme, "Card network", "Authorization requests and responses")
    System_Ext(case, "Case management", "Tracks investigations")
    Rel(scheme, fraud, "Sends authorization events", "ISO 8583 via gateway")
    Rel(fraud, scheme, "Returns risk decision")
    Rel(analyst, fraud, "Reviews alerts")
    Rel(fraud, case, "Opens fraud case", "REST")
```

# Data Lifecycle Diagram

Mermaid type: `stateDiagram-v2` (Close fit). Source: Modeling-Diagraming.md, section "Data warehouse".

It answers how long data is retained, when it must be deleted, and which regulatory or operational obligations apply.

## Example 1: Simple - card transaction retention
```mermaid
stateDiagram-v2
    [*] --> Active: posted
    Active --> Archived: 90 days after posting
    Archived --> Deleted: 7 years after posting
    Deleted --> [*]
```

## Example 2: Realistic - customer data after account closure
```mermaid
stateDiagram-v2
    [*] --> Collected
    Collected --> Active: account opened
    Active --> Dormant: no activity for 24 months
    Active --> Closed: account closed
    Dormant --> Closed: customer exit
    Closed --> LegalHold: open AML case
    LegalHold --> Anonymised: hold lifted
    Closed --> Anonymised: retention ends, no hold
    Anonymised --> Deleted: 5 years after closure (GDPR)
    Deleted --> [*]
```

# Process Diagram (BPMN)

Mermaid type: `flowchart` (Approximate fit). Source: Modeling-Diagraming.md, section "Business Processes, Workflows & Decisions".

It answers how a business process works, what happens next, and where decisions, exceptions, and parallel activities occur.

## Example 1: Simple - Consumer loan application

```mermaid
flowchart TD
    Start([Application received]) --> Check[Check credit score]
    Check --> Score{Score above threshold?}
    Score -- No --> Reject[Send rejection letter]
    Score -- Yes --> Afford[Assess affordability]
    Afford --> Afforded{Affordable?}
    Afforded -- No --> Reject
    Afforded -- Yes --> Offer[Issue offer]
    Offer --> Offered([Offer sent])
    Reject --> Closed([Application closed])
```

## Example 2: Realistic - Card dispute with parallel checks

```mermaid
flowchart TD
    Start([Card dispute received]) --> Triage[Triage dispute]
    Triage --> Valid{Within 120 days?}
    Valid -- No --> Reject[Reject dispute]
    Valid -- Yes --> Fork{{Parallel checks}}
    Fork --> Fraud[Fraud review]
    Fork --> Merchant[Request merchant evidence]
    Fraud --> Join{{Decision ready}}
    Merchant --> Join
    Join --> Liable{Customer liable?}
    Liable -- No --> Credit[[Chargeback and credit account]]
    Liable -- Yes --> Notify[Notify customer]
    Credit --> Closed([Dispute closed])
    Notify --> Closed
    Reject --> Closed
```

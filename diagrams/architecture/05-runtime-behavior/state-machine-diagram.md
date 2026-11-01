# State Machine Diagram (UML)

Mermaid type: `stateDiagram-v2` (Native fit). Source: Modeling-Diagraming.md, section "Runtime Behavior, Interactions & State".

Models states, events, guards, actions, and transitions for an entity, answering which states are valid and which transitions are permitted.

## Example 1: Simple - Payment states
```mermaid
stateDiagram-v2
    [*] --> Initiated
    Initiated --> Authorized: authorize [funds available]
    Initiated --> Rejected: authorize [insufficient funds]
    Authorized --> Settled: settle / post to ledger
    Authorized --> Failed: timeout after 24 h
    Settled --> [*]
    Rejected --> [*]
    Failed --> [*]
```

## Example 2: Realistic - Payment card lifecycle
```mermaid
stateDiagram-v2
    [*] --> Ordered
    Ordered --> Inactive: card produced and dispatched
    Inactive --> Active: PIN set and card activated
    Active --> Blocked: fraud alert
    Blocked --> Active: analyst clears alert
    Blocked --> Closed: fraud confirmed
    Active --> Expired: expiry date reached
    Expired --> Closed: replacement issued
    Closed --> [*]
```

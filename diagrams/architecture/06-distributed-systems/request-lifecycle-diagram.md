# Request Lifecycle Diagram

Mermaid type: `sequenceDiagram` (Close fit). Source: Modeling-Diagraming.md, section "Distributed systems".

Traces a request through authentication, validation, orchestration, processing, storage, and response generation.

## Example 1: Simple - Account balance query through gateway
```mermaid
sequenceDiagram
    participant App as Mobile app
    participant GW as API gateway
    participant Auth as Identity service
    participant Svc as Accounts service
    participant DB as Accounts DB
    App->>GW: GET account balance
    GW->>Auth: Validate token
    Auth-->>GW: Valid
    GW->>Svc: Forward request
    Svc->>DB: Select balance
    DB-->>Svc: Row
    Svc-->>GW: 200 OK
    GW-->>App: 200 OK with balance
```

## Example 2: Realistic - Card authorization with early rejection and cache path
```mermaid
sequenceDiagram
    participant POS as Card acceptor gateway
    participant GW as API gateway
    participant Val as Request validator
    participant Auth as Authorization service
    participant Cache as Card status cache
    participant DB as Cards DB
    POS->>GW: POST authorization
    GW->>Val: Check schema and mandatory fields
    alt Invalid request
        Val-->>GW: 400 Bad Request
        GW-->>POS: Rejected at gateway
    else Valid
        Val->>Auth: Forward authorization
        Auth->>Cache: Get card status
        alt Cache miss
            Cache->>DB: Read card status
            DB-->>Cache: Status
        end
        Cache-->>Auth: Status ACTIVE
        Auth-->>GW: 200 Approved
        GW-->>POS: Response
    end
```

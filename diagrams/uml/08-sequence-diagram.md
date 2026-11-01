# Sequence diagram

Mermaid type: `sequenceDiagram` (Native fit). UML type: sequence diagram.

Shows messages exchanged between participants over time.

## Description

Ordered exchange of messages between participants over time, with fragments for alternatives, loops, and parallel flows.

## Example usages

- API call flows and request/response chains
- Authentication and authorization handshakes
- Error and retry handling scenarios
- Integration flows between services

## Example 1: Simple - Create an order

```mermaid
sequenceDiagram
    participant C as Customer
    participant API as Orders API
    C->>API: POST /orders
    API-->>C: 201 Created
```

## Example 2: Complex - Payment with alternative and loop fragments

```mermaid
sequenceDiagram
    participant C as Customer
    participant API as Orders API
    participant PAY as Payment service
    participant DB as Orders DB
    C->>API: POST /orders
    API->>DB: insert order (PENDING)
    alt payment authorized
        API->>PAY: authorize(amount)
        PAY-->>API: approved
        API->>DB: update status PAID
        API-->>C: 201 Created
    else payment declined
        PAY-->>API: declined
        API-->>C: 402 Payment Required
    end
    loop every 5 min
        API->>PAY: reconcile()
    end
```

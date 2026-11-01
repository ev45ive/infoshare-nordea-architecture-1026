# Flowchart

Flowcharts show process steps, decisions, and flow of control.

## Simple example: order payment

```mermaid
flowchart LR
    A[Customer places order] --> B{Payment valid?}
    B -- Yes --> C[Ship order]
    B -- No --> D[Notify customer]
```

## Complex example: incident handling with escalation

```mermaid
flowchart TD
    Start([Incident reported]) --> Triage{Severity?}
    Triage -- P1 --> Page[Page on-call SRE]
    Triage -- P2/P3 --> Ticket[Create ticket]
    Page --> Mitigate[Mitigate service]
    Ticket --> Queue[Add to backlog]
    Mitigate --> Verify{Service restored?}
    Verify -- No --> Escalate[Escalate to incident commander]
    Escalate --> Mitigate
    Verify -- Yes --> Review[Post-incident review]
    Queue --> Review
    Review --> End([Close])
```

## Complex example: architecture with subgraphs

```mermaid
flowchart LR
    subgraph Client
        Web[Web app]
    end
    subgraph Cloud
        API[API gateway] --> Svc[Order service]
        Svc --> DB[(Orders DB)]
    end
    Web -->|HTTPS| API
```

# Message Routing Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Integration, APIs & Distributed Systems".

Shows routing, filtering, transformation, enrichment, aggregation, and delivery paths, including where retries and dead-letter handling apply.

## Example 1: Simple - Content-based router for payment types

```mermaid
flowchart LR
    In["Payment intake queue"] --> Router{"Content-based router<br/>by payment type"}
    Router -- "SEPA credit transfer" --> SEPA["SEPA gateway"]
    Router -- "Instant payment" --> Inst["Instant payments gateway"]
    Router -- "Card settlement" --> Card["Card settlement service"]
    Router -- "Unknown type" --> DLQ[("Dead-letter queue")]
```

## Example 2: Realistic - Validation, enrichment and routing of outgoing payments

```mermaid
flowchart LR
    Src["Payment initiation channel"] --> Val["Schema validator"]
    Val -- "invalid" --> DLQ[("payments.dlq")]
    Val -- "valid" --> Enr["Enricher: customer and limits lookup"]
    Enr --> Router{"Router by currency and amount"}
    Router -- "EUR, under 10k" --> Fast["Real-time clearing"]
    Router -- "EUR, 10k or more" --> Screen["Sanctions screening"]
    Router -- "Other currency" --> Swift["SWIFT gateway"]
    Fast -- "retry 3x, then" --> DLQ
    Screen -- "hit: manual review" --> Case["Compliance case queue"]
    Screen -- "clear" --> Clr["Clearing house"]
```

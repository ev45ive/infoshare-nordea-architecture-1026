# Fault Tree Analysis (FTA)

Mermaid type: `flowchart` TD with AND/OR gate nodes (Approximate fit). Source: Modeling-Diagraming.md, section "Reliability, Performance & Quality Attributes".

Decomposes an undesirable failure into contributing events and conditions joined by logical gates, showing which combinations of failures could cause an outage.

## Example 1: Simple - database and failover both fail

```mermaid
flowchart TD
    TOP["Card authorization outage"] --> AND1{{"AND"}}
    AND1 --> E1["Primary database unavailable"]
    AND1 --> E2["Standby failover fails"]
```

## Example 2: Realistic - card payments rejected

```mermaid
flowchart TD
    TOP["Card payments rejected"] --> OR1((OR))
    OR1 --> E1["Authorization service timeouts"]
    OR1 --> AND1{{"AND"}}
    OR1 --> E2["Bad routing config deployed"]
    AND1 --> E3["Gateway TLS certificate expired"]
    AND1 --> E4["Expiry alert suppressed"]
```

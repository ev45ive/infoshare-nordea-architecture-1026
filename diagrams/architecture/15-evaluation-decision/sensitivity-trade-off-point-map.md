# Sensitivity / Trade-off Point Map (ATAM)

Mermaid type: `mindmap` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evaluation & Decision Support".

Identifies architectural decisions that strongly influence one or several quality attributes, showing which decisions are sensitive to change and where one attribute harms another.

## Example 1: Simple - Payments utility tree

```mermaid
mindmap
  root((Utility tree))
    Latency
      Balance lookup under 200 ms at peak
        Cache of account balances
          Sensitivity point for latency
        Synchronous fraud score
          Trade-off point with fraud detection
    Availability
      Payment API 99.95 percent monthly
        Active-active across two zones
          Sensitivity point for availability
```

## Example 2: Realistic - Card authorization utility tree

```mermaid
mindmap
  root((Card authorization utility))
    Performance
      Authorization decision under 300 ms at p95
        Card limit cache in memory
          Sensitivity point for latency
        Synchronous 3DS risk check
          Trade-off point for security versus latency
    Availability
      Authorization available 99.99 percent
        Active-active across two regions
          Trade-off point for cost and consistency
        Stand-in processing when core is down
          Sensitivity point for availability
    Security
      Card data encrypted end to end
        Tokenization at gateway
          Sensitivity point for PCI scope
```

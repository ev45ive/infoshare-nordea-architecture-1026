# Capacity / Queuing Model

Mermaid type: `xychart-beta` (load vs latency) + `flowchart` (queues) (Close fit). Source: Modeling-Diagraming.md, section "Reliability, Performance & Quality Attributes".

Represents arrival rates, service capacity, queues, and workers to show where bottlenecks form and how latency and throughput change as load increases.

## Example 1: Simple - latency curve vs requests per second

```mermaid
xychart-beta
    title "Authorization p95 latency vs load"
    x-axis "Requests per second" 500 --> 2500
    y-axis "p95 latency ms" 0 --> 800
    line [120, 150, 210, 380, 760]
```

## Example 2: Realistic - payment queue with three workers

```mermaid
flowchart LR
    ARR["Payment arrivals 1800 msg/s"] --> Q[("Payment queue")]
    Q --> W1["Worker 1 400 msg/s"] & W2["Worker 2 400 msg/s"] & W3["Worker 3 400 msg/s"]
    W1 & W2 & W3 --> LED["Ledger posting 1200 msg/s capacity"]
```

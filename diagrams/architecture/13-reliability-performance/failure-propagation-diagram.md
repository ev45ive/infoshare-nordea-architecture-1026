# Failure Propagation Diagram

Mermaid type: `flowchart` LR with timeout and fallback edges (Close fit). Source: Modeling-Diagraming.md, section "Reliability, Performance & Quality Attributes".

Shows how failures, congestion, timeouts, or resource exhaustion spread through dependencies, and where isolation or fallback behavior should stop the spread.

## Example 1: Simple - fraud service slowdown exhausts threads

```mermaid
flowchart LR
    FRAUD["Fraud scoring slow 8 s"] -->|"timeout 2 s"| AUTH["Authorization service"]
    AUTH -->|"threads blocked"| POOL["Thread pool exhausted"]
    POOL -->|"declines to card network"| CARD["Card declines spike"]
    AUTH -.->|"circuit open"| FB["Rule-based fallback score"]
```

## Example 2: Realistic - cache loss overloads account database

```mermaid
flowchart LR
    REDIS["Session cache node lost"] -->|"100 percent cache miss"| ACCT["Account service"]
    ACCT -->|"5x read load"| DB[("Core account DB")]
    DB -->|"connection pool saturated"| ACCT
    ACCT -.->|"bulkhead 200 req/s"| SHED["Shed excess with HTTP 429"]
```

# Quality Attribute Scenario Diagram

Mermaid type: `requirementDiagram` (Close fit). Source: Modeling-Diagraming.md, section "Reliability, Performance & Quality Attributes".

Shows what should happen under a specific operational condition and how the quality requirement will be verified.

## Example 1: Simple - availability target

```mermaid
requirementDiagram

requirement availability_req {
    id: QA-AVL-01
    text: Card authorization service available 99.9 percent during business hours
    risk: high
    verifymethod: analysis
}

element card_auth_service {
    type: service
}

card_auth_service - satisfies -> availability_req
```

## Example 2: Realistic - peak payment latency scenario

```mermaid
requirementDiagram

performanceRequirement payment_latency {
    id: QA-PERF-02
    text: Card authorization p95 under 300 ms at 2000 TPS peak
    risk: high
    verifymethod: test
}

element merchant_burst {
    type: stimulus
}

element peak_season_load {
    type: environment
}

element auth_service {
    type: artifact
}

merchant_burst - traces -> payment_latency
peak_season_load - traces -> payment_latency
auth_service - satisfies -> payment_latency
```
</content>
</invoke>

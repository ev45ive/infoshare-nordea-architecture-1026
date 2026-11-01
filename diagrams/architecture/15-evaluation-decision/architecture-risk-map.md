# Architecture Risk Map

Mermaid type: `quadrantChart` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evaluation & Decision Support".

Places risks against impact and likelihood, showing which architectural risks to investigate first and where verification effort belongs.

## Example 1: Simple - Core platform risks

```mermaid
quadrantChart
    title Architecture risks
    x-axis Low likelihood --> High likelihood
    y-axis Low impact --> High impact
    quadrant-1 Investigate first
    quadrant-2 Monitor closely
    quadrant-3 Accept
    quadrant-4 Mitigate cheaply
    Legacy core dependency: [0.75, 0.9]
    Vendor lock-in: [0.6, 0.7]
    Skills gap: [0.8, 0.45]
    Single cloud region: [0.2, 0.85]
```

## Example 2: Realistic - Platform modernization risks

```mermaid
quadrantChart
    title Platform modernization risks
    x-axis Low likelihood --> High likelihood
    y-axis Low impact --> High impact
    quadrant-1 Investigate first
    quadrant-2 Monitor closely
    quadrant-3 Accept
    quadrant-4 Mitigate cheaply
    Mainframe batch window overrun: [0.85, 0.8]
    Real-time payments scheme change: [0.5, 0.95]
    Cloud egress cost growth: [0.7, 0.3]
    Key engineers leaving: [0.6, 0.55]
    Regulatory reporting data quality: [0.35, 0.9]
```

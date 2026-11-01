# Goal Realization Diagram (ArchiMate)

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Enterprise Architecture & Business Strategy".

Shows how goals are refined and supported by outcomes, requirements, and other goals, answering how architectural requirements contribute to business objectives.

## Example 1: Simple - requirements realizing goals

```mermaid
flowchart TD
    G1["Goal: Faster customer onboarding"]
    G2["Goal: Lower fraud losses"]
    R1["Requirement: Electronic ID verification"]
    R2["Requirement: Real-time sanctions screening"]
    O1["Outcome: Account opened within one day"]
    R1 -->|realizes| G1
    R2 -->|realizes| G2
    O1 -->|realizes| G1
```

## Example 2: Realistic - conflicting goals in a payment hub

```mermaid
flowchart TD
    G1["Goal: Real-time payments for retail customers"]
    G2["Goal: Zero tolerance for sanctions breaches"]
    G3["Goal: Settle payments within 10 seconds"]
    R1["Requirement: Event-driven payment hub"]
    R2["Requirement: Synchronous sanctions check before release"]
    R3["Requirement: Pre-funded settlement accounts"]
    R1 -->|realizes| G1
    R2 -->|realizes| G2
    R3 -->|realizes| G3
    R2 -.->|may delay| G3
```

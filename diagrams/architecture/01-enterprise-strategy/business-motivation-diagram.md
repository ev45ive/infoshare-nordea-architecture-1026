# Business Motivation Diagram (ArchiMate)

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Enterprise Architecture & Business Strategy".

Connects stakeholders, drivers, assessments, goals, outcomes, principles, and requirements to answer why the architecture is changing and which objectives, pressures, and constraints justify the change.

## Example 1: Simple - regulation driving an open-API goal

```mermaid
flowchart TD
    D1["Driver: PSD2 open banking regulation"]
    G1["Goal: Open APIs for third-party providers"]
    R1["Requirement: Expose account information API"]
    A1["Assessment: API gateway lacks consent management"]
    D1 -->|influences| G1
    G1 -->|realized by| R1
    A1 -->|associated with| R1
```

## Example 2: Realistic - cost and compliance drivers

```mermaid
flowchart TD
    D1["Driver: Cost pressure on legacy mainframe"]
    D2["Driver: DORA operational resilience obligations"]
    S1["Assessment: Batch regulatory reporting takes 14 hours"]
    P1["Principle: Data is owned once and reused"]
    G1["Goal: Move regulatory reporting to cloud data platform"]
    G2["Goal: Reduce mainframe run cost by 30%"]
    R1["Requirement: Daily regulatory data within 4 hours"]
    R2["Requirement: Audit trail for every report"]
    D1 -->|influences| G2
    D2 -->|influences| G1
    S1 -->|supports| D1
    G1 -->|realized by| R1
    G1 -->|realized by| R2
    P1 -.->|constrains| R1
```

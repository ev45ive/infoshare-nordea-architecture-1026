# Business–Application Alignment (Capability-Service Map) Diagram

Mermaid type: `block-beta` (Close fit). Source: Modeling-Diagraming.md, section "Enterprise Architecture & Business Strategy".

Maps business capabilities, processes, and services to supporting applications, showing which applications support which business functions and where gaps or redundant systems exist.

## Example 1: Simple - capability to application grid

```mermaid
block-beta
    columns 3
    h1["Capability"] h2["Core Banking"] h3["Payment Hub"]
    c1["Account management"] a1["Primary"] a2["Not used"]
    c2["Domestic payments"] a3["Partial"] a4["Primary"]
    classDef primary fill:#2e7d32,color:#fff
    classDef partial fill:#f9a825,color:#000
    class a1 primary
    class a4 primary
    class a3 partial
```

## Example 2: Realistic - card dispute capability with a duplicate application

```mermaid
block-beta
    columns 6
    h0["Capability"] h1["Core Banking"] h2["CRM"] h3["Card Platform"] h4["Legacy Dispute Tool"] h5["Data Platform"]
    c1["Customer servicing"] s1["Supports"] s2["Primary"] s3["-"] s4["-"] s5["-"]
    c2["Card dispute handling"] t1["-"] t2["-"] t3["Primary"] t4["Duplicate"] t5["-"]
    c3["Regulatory reporting"] r1["Source"] r2["-"] r3["-"] r4["-"] r5["Primary"]
    classDef primary fill:#2e7d32,color:#fff
    classDef duplicate fill:#c62828,color:#fff
    class s2 primary
    class t3 primary
    class r5 primary
    class t4 duplicate
```

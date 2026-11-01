# Dependency Structure Matrix (DSM)

Mermaid type: `block-beta` (Approximate fit). Source: Modeling-Diagraming.md, section "Architecture Evaluation & Decision Support".

A square matrix visualizing dependencies between components, showing where coupling concentrates, which elements can be separated, and which cycles block independent evolution.

## Example 1: Simple - Payments service dependencies

Row depends on column; `1` marks a dependency, red cells form a cycle.

```mermaid
block-beta
  columns 5
  h0["DSM"] h1["Payments"] h2["Accounts"] h3["Ledger"] h4["Fraud"]
  r1["Payments"] d1["-"] e1["0"] f1["1"] g1["1"]
  r2["Accounts"] d2["0"] e2["-"] f2["1"] g2["0"]
  r3["Ledger"] d3["1"] e3["0"] f3["-"] g3["0"]
  r4["Fraud"] d4["0"] e4["0"] f4["0"] g4["-"]
  classDef cyclic fill:#f8d7da,stroke:#b02a37
  class f1 cyclic
  class d3 cyclic
```

## Example 2: Realistic - Customer onboarding dependencies

```mermaid
block-beta
  columns 6
  h0["DSM"] h1["Onboarding"] h2["KYC"] h3["Registry"] h4["Credit"] h5["Core"]
  a0["Onboarding"] a1["-"] a2["1"] a3["1"] a4["1"] a5["0"]
  b0["KYC"] b1["0"] b2["-"] b3["0"] b4["0"] b5["0"]
  c0["Registry"] c1["1"] c2["0"] c3["-"] c4["0"] c5["1"]
  d0["Credit"] d1["0"] d2["0"] d3["1"] d4["-"] d5["1"]
  e0["Core"] e1["0"] e2["0"] e3["0"] e4["0"] e5["-"]
  classDef cyclic fill:#f8d7da,stroke:#b02a37
  class a3 cyclic
  class c1 cyclic
```

# Migration Roadmap / Plateau Diagram (ArchiMate)

Mermaid type: `gantt` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evolution, Migration & Planning".

Shows architectural plateaus, implementation work, gaps, and transitions over time, answering in what order changes should occur and which dependencies constrain the sequence.

## Example 1: Simple - Payments platform plateaus

```mermaid
gantt
    title Payments platform plateaus
    dateFormat YYYY-MM-DD
    section Plateau 1 Foundation
    Landing zone and network        :done, p1a, 2027-01-04, 60d
    Event bus and API gateway       :p1b, after p1a, 45d
    section Plateau 2 Pilot
    Card pilot on new hub           :p2a, after p1b, 60d
    section Plateau 3 Cutover
    Migrate all card traffic        :p3a, after p2a, 45d
    Retire legacy switch            :milestone, p3b, after p3a, 0d
```

## Example 2: Realistic - Core banking migration with plateaus

```mermaid
gantt
    title Core banking migration roadmap
    dateFormat YYYY-MM-DD
    axisFormat %b %Y
    section Plateau A - Mainframe
    Batch stabilisation                 :done, a1, 2027-01-04, 90d
    section Plateau B - Coexistence
    Customer master to new platform     :b1, after a1, 120d
    Product catalogue migration         :b2, after a1, 90d
    Dual-run deposit accounts           :crit, b3, after b1, 120d
    section Plateau C - Target
    Regulatory reporting cutover        :c1, after b3, 60d
    Mainframe decommission              :milestone, c2, after c1, 0d
```

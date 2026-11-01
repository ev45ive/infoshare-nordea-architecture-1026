# Implementation and migration viewpoint

ArchiMate viewpoint: Implementation and migration (migration roadmap, plateaus). Mermaid type: `gantt` (Approximate fit).

Mermaid has no ArchiMate support. Plateaus and work packages are drawn as gantt sections and tasks. Plateau states and gaps between them are not modeled.

## Description

Shows how the architecture moves from the baseline to the target through transition states (plateaus), with work packages and milestones on a timeline.

## Example usages

- Planning a migration roadmap across plateaus
- Showing when a transition architecture is live
- Tracking work packages against plateaus
- Communicating milestones to programme boards

## Example 1: Simple - Baseline and target plateaus

```mermaid
gantt
    title Migration plateaus
    dateFormat YYYY-MM-DD
    section Plateaus
    Baseline           :done, p0, 2026-01-01, 2026-06-30
    Target             :p1, 2026-07-01, 2026-12-31
```

## Example 2: Complex - Payments migration with transition work

```mermaid
gantt
    title Payments migration roadmap
    dateFormat YYYY-MM-DD
    section Plateau 1 Baseline
    Legacy payments running       :done, base, 2026-01-01, 2026-03-31
    section Transition
    Build payment gateway         :active, tr1, 2026-04-01, 2026-06-30
    Dual running with legacy      :tr2, 2026-07-01, 2026-09-30
    section Plateau 2 Target
    Retire legacy payments        :milestone, m1, 2026-10-01, 0d
    Target payments platform      :p2, 2026-10-01, 2026-12-31
```

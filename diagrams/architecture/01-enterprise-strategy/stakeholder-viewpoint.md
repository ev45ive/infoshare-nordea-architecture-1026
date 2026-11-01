# Stakeholder Viewpoint (ArchiMate)

Mermaid type: `quadrantChart` (Close fit). Source: Modeling-Diagraming.md, section "Enterprise Architecture & Business Strategy".

Maps stakeholders to their concerns, drivers, and desired outcomes to show who cares about the change and which competing interests must be reconciled.

## Example 1: Simple - influence vs interest

```mermaid
quadrantChart
    title Stakeholders for mortgage system change
    x-axis Low interest --> High interest
    y-axis Low influence --> High influence
    quadrant-1 Manage closely
    quadrant-2 Keep satisfied
    quadrant-3 Monitor
    quadrant-4 Keep informed
    Compliance Officer: [0.30, 0.90]
    Chief Risk Officer: [0.55, 0.80]
    Mortgage Advisors: [0.85, 0.40]
    Branch Managers: [0.75, 0.25]
    Customers: [0.90, 0.10]
```

## Example 2: Realistic - competing concerns on an instant payments change

```mermaid
quadrantChart
    title Competing concerns on instant payments change
    x-axis Prefers controls --> Prefers speed of delivery
    y-axis Low risk appetite --> High risk appetite
    quadrant-1 Pragmatic sponsors
    quadrant-2 Cautious gatekeepers
    quadrant-3 Risk-averse reviewers
    quadrant-4 Delivery pressure
    Product Owner: [0.90, 0.80]
    Head of Operations: [0.35, 0.60]
    Internal Audit: [0.20, 0.40]
    Chief Compliance Officer: [0.15, 0.25]
    Chief Information Security Officer: [0.25, 0.20]
```

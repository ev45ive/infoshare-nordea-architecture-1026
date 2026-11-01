# Application Portfolio Map

Mermaid type: `quadrantChart` (Close fit). Source: Modeling-Diagraming.md, section "Enterprise Architecture & Business Strategy".

Visualizes applications by business importance and technical health to show which applications to invest in, modernize, consolidate, or retire.

## Example 1: Simple - value vs technical health

```mermaid
quadrantChart
    title Application portfolio by business value and technical health
    x-axis Low technical health --> High technical health
    y-axis Low business value --> High business value
    quadrant-1 Invest
    quadrant-2 Modernize
    quadrant-3 Retire
    quadrant-4 Tolerate
    Core Banking Mainframe: [0.20, 0.90]
    Mobile Banking App: [0.85, 0.80]
    Legacy Dispute Tool: [0.15, 0.20]
    Survey Tool: [0.80, 0.15]
```

## Example 2: Realistic - retail banking portfolio review

```mermaid
quadrantChart
    title Retail banking portfolio review
    x-axis Low technical health --> High technical health
    y-axis Low business value --> High business value
    quadrant-1 Invest
    quadrant-2 Modernize
    quadrant-3 Consolidate or retire
    quadrant-4 Tolerate
    Core Banking Mainframe: [0.15, 0.95]
    Payment Hub: [0.80, 0.90]
    Card Management: [0.70, 0.75]
    Duplicate CRM Tool B: [0.35, 0.30]
    Legacy Dispute Tool: [0.10, 0.25]
    Regulatory Reporting Data Mart: [0.60, 0.65]
    Intranet Portal: [0.75, 0.10]
```

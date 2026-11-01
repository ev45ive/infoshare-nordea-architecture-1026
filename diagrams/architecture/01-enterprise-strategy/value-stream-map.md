# Value Stream Map (ArchiMate / business architecture)

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Enterprise Architecture & Business Strategy".

Models the stages through which the organization creates value for customers, showing where value is created and where delays, handoffs, and improvement opportunities sit.

## Example 1: Simple - loan origination

```mermaid
flowchart LR
    A["Application intake<br/>touch time 10 min"] -->|"wait 1 day"| B["Credit check<br/>touch time 2 h"]
    B -->|"wait 3 days"| C["Approval<br/>touch time 30 min"]
    C -->|"wait 2 days"| D["Signing<br/>touch time 15 min"]
    D --> E["Loan disbursed"]
```

## Example 2: Realistic - card dispute handling

```mermaid
flowchart LR
    A["Customer dispute<br/>touch time 5 min"] --> B["Case logged<br/>manual re-keying 20 min"]
    B -->|"wait 2 days"| C["Fraud review<br/>touch time 45 min"]
    C -->|"handoff to card scheme"| D["Chargeback filed<br/>touch time 15 min"]
    D -->|"wait 30 days"| E["Scheme decision"]
    E --> F["Customer credited"]
    style B fill:#fdd,stroke:#c00
```

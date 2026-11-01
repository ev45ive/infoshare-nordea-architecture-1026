# Use Case Diagram (UML)

Mermaid type: `flowchart` (Approximate fit). Source: Modeling-Diagraming.md, section "Business Processes, Workflows & Decisions".

It answers what functionality the system exposes and who initiates or participates in each interaction.

## Example 1: Simple - Mobile banking customer

```mermaid
flowchart LR
    Customer[Retail customer]
    Core[Core banking]

    subgraph MB[Mobile banking]
        UC1([View balance])
        UC2([Transfer money])
        UC3([Pay bill])
    end

    Customer --- UC1
    Customer --- UC2
    Customer --- UC3
    UC2 --- Core
    UC3 --- Core
```

## Example 2: Realistic - Customer onboarding with include relations

```mermaid
flowchart LR
    RM[Relationship manager]
    Compliance[Compliance officer]
    KYC[eKYC provider]

    subgraph ONB[Customer onboarding platform]
        UC1([Open account])
        UC2([Verify identity])
        UC3([Screen sanctions])
        UC4([Approve onboarding])
    end

    RM --- UC1
    RM --- UC4
    Compliance --- UC4
    UC1 -. include .-> UC2
    UC1 -. include .-> UC3
    UC2 --- KYC
```

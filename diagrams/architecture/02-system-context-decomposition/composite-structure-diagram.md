# Composite Structure Diagram (UML)

Mermaid type: `block-beta` (Approximate fit). Source: Modeling-Diagraming.md, section "Boundaries & Decomposition".

Source gives no description for this item. The diagram shows a system built from nested parts and the connections between them.

## Example 1: Simple - ATM with parts

```mermaid
block-beta
    columns 2
    block:atm:2
        columns 3
        reader["Card reader"]
        cash["Cash unit"]
        screen["Screen"]
    end
    controller["ATM controller"]:2
    reader --> controller
    cash --> controller
    screen --> controller
```

## Example 2: Realistic - card authorization engine

```mermaid
block-beta
    columns 3
    block:auth:3
        columns 3
        api["Authorization API"]
        rules["Rule engine"]
        velocity["Velocity counter"]
    end
    ledger["Ledger port"]
    scheme["Scheme gateway"]
    api --> rules
    rules --> velocity
    rules --> ledger
    api --> scheme
```

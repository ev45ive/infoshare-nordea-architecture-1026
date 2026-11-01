# Object diagram

Mermaid type: `flowchart` (Approximate fit). UML type: object diagram.

Mermaid has no object diagram. Instances are drawn as flowchart nodes with `name : Class` labels and slot values.

## Description

Snapshot of concrete instances and their links at one point in time, showing actual slot values.

## Example usages

- Illustrating a class model with concrete example data
- Debugging the state of objects at runtime
- Showing test fixtures or sample messages
- Explaining a complex object graph

## Example 1: Simple - One customer and one order

```mermaid
flowchart LR
    alice["alice : Customer<br/>name = Alice"]
    order1["order1 : Order<br/>id = 1001<br/>status = PAID"]
    alice -->|places| order1
```

## Example 2: Complex - Snapshot of an order with lines

```mermaid
flowchart LR
    subgraph snapshot["Snapshot at 2026-11-01 10:00"]
        alice["alice : Customer<br/>tier = GOLD"]
        order1["order1 : Order<br/>total = 250"]
        order2["order2 : Order<br/>total = 40"]
        line1["line1 : OrderLine<br/>sku = A-12"]
    end
    alice -->|places| order1
    alice -->|places| order2
    order1 -->|contains| line1
```

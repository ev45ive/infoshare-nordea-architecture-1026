# Trade-off Map

Mermaid type: `radar-beta` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evaluation & Decision Support".

Visualizes competing quality attributes and architectural alternatives, showing what each option optimizes or sacrifices.

## Example 1: Simple - Payments platform hosting

```mermaid
radar-beta
  title Payments platform hosting
  axis cost["Cost efficiency"], speed["Time to change"], control["Control"], resilience["Resilience"], security["Security"]
  curve cloud["Public cloud"]{3, 5, 2, 5, 4}
  curve onprem["On-premise"]{2, 2, 5, 3, 4}
  max 5
  min 0
```

## Example 2: Realistic - Card authorization engine options

```mermaid
radar-beta
  title Card authorization options
  axis lat["Latency"], comp["Compliance fit"], ttm["Time to market"], cost["Cost efficiency"], exit["Exit flexibility"]
  curve build["Build in-house"]{4, 5, 1, 3, 5}
  curve buy["Buy vendor"]{3, 3, 5, 3, 1}
  curve hybrid["Hybrid"]{4, 4, 3, 4, 3}
  max 5
  min 0
```

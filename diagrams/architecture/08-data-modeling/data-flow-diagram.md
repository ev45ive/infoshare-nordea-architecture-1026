# Data Flow Diagram (DFD)

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Data Architecture & Information Modeling".

Shows where information originates, how it moves and is transformed through processes and data stores, and which flows cross system boundaries.

## Example 1: Simple - card payment authorization
```mermaid
flowchart LR
    M["Merchant"] -->|"card payment request"| P1(("1.0 Authorize payment"))
    P1 -->|"authorization request"| CN["Card network"]
    CN -->|"decision"| P1
    P1 -->|"authorization record"| D1[("Authorization log")]
    P1 -->|"approved or declined"| M
```

## Example 2: Realistic - monthly regulatory reporting
```mermaid
flowchart LR
    CB["Core banking"] -->|"daily balances"| P1(("1.0 Extract"))
    P1 -->|"raw extracts"| D1[("Staging area")]
    D1 --> P2(("2.0 Validate and transform"))
    P2 -->|"validated positions"| D2[("Regulatory data mart")]
    P2 -->|"rejected records"| D3[("Exception queue")]
    D2 --> P3(("3.0 Build report"))
    P3 -->|"reporting file"| FS["Financial supervisor"]
    D3 --> DO["Data operations"]
```

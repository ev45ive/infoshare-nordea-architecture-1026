# Hexagonal / Ports-and-Adapters Diagram

Mermaid type: `flowchart` (Approximate fit). Source: Modeling-Diagraming.md, section "Boundaries & Decomposition".

Source gives no description for this item. The diagram shows a core domain isolated from external systems through input and output ports, with adapters plugged into those ports.

## Example 1: Simple - loan domain core with REST and Kafka adapters

```mermaid
flowchart LR
    subgraph core["Loan domain core"]
        inPort(["Input port: ApplyForLoan"])
        domain["Loan rules and decisions"]
        outPort(["Output port: LoanRepository"])
        inPort --> domain
        domain --> outPort
    end
    rest["REST adapter<br/>channel API"] --> inPort
    kafka["Kafka adapter<br/>scoring events"] --> inPort
    outPort --> jdbc["JDBC adapter<br/>PostgreSQL"]
```

## Example 2: Realistic - payment core with card scheme adapter and test double

```mermaid
flowchart LR
    subgraph core["Payment domain core"]
        authIn(["Input port: AuthorizePayment"])
        policy["Authorization policy"]
        schemeOut(["Output port: CardScheme"])
        ledgerOut(["Output port: Ledger"])
        authIn --> policy
        policy --> schemeOut
        policy --> ledgerOut
    end
    api["REST adapter<br/>merchant gateway"] --> authIn
    schemeOut --> scheme["Card scheme adapter<br/>ISO 8583 gateway"]
    schemeOut -.-> stub["Test double adapter<br/>in-memory scheme"]
    ledgerOut --> ledger["Ledger adapter<br/>core banking API"]
```

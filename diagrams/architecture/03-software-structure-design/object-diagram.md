# Object Diagram (UML)

Mermaid type: `flowchart` (Approximate fit). Source: Modeling-Diagraming.md, section "Software Structure, Object Models & Design".

The diagram answers what a valid runtime object structure looks like and whether the model can represent a specific scenario.

## Example 1: Simple - customer snapshot
```mermaid
flowchart LR
    c1["customer:Customer<br/>id = C-1001<br/>name = Anna Lindqvist"]
    a1["account:Account<br/>iban = FI21 5000 0000 1234<br/>balance = 1 200.00 EUR"]
    a2["savings:SavingsAccount<br/>balance = 15 000.00 EUR"]
    c1 -->|owns| a1
    c1 -->|owns| a2
```

## Example 2: Realistic - card payment at a point in time
```mermaid
flowchart LR
    p["payment:PaymentOrder<br/>status = AUTHORIZED<br/>amount = 84.50 EUR"]
    card["card:CardAccount<br/>token = tok_9f2c<br/>status = ACTIVE"]
    m["merchant:Merchant<br/>mcc = 5411"]
    l1["entry1:LedgerEntry<br/>debit 84.50 EUR"]
    l2["entry2:LedgerEntry<br/>credit 84.50 EUR"]
    p -->|paid with| card
    p -->|to| m
    p -->|posted as| l1
    p -->|posted as| l2
```

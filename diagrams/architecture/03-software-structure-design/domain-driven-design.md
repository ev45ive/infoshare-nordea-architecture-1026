# Domain Driven Design

Mermaid type: `mindmap` (Approximate fit). Source: Modeling-Diagraming.md, section "Software Structure, Object Models & Design".

The file shows how the banking domain is split into bounded contexts and how an aggregate groups the entities that must change together.

## Example 1: Simple - bounded contexts
```mermaid
mindmap
  root((Nordea Retail Domain))
    Customer Onboarding
      Party
      KYC Case
    Payments
      Payment Order
      Settlement Instruction
    Cards
      Card Account
      Authorization
    Core Banking
      Ledger
      Account
```

## Example 2: Realistic - account aggregate
```mermaid
mindmap
  root((Account Context))
    Aggregate Account
      Account root
        IBAN
        Status
      Entities
        Transaction
        Hold
      Invariant
        Available balance not below overdraft limit
    Aggregate Customer
      Customer root
      Address value object
```

# Class Diagram (UML)

Mermaid type: `classDiagram` (Native fit). Source: Modeling-Diagraming.md, section "Software Structure, Object Models & Design".

The diagram answers what the types are and how they relate, and which abstractions own which responsibilities.

## Example 1: Simple - account inheritance
```mermaid
classDiagram
    class Account {
        +String iban
        +Money balance
        +deposit(amount) void
        +withdraw(amount) void
    }
    class SavingsAccount {
        +Decimal interestRate
        +accrueInterest() void
    }
    class Customer {
        +String customerId
        +String name
    }
    Account <|-- SavingsAccount
    Customer "1" --> "*" Account : owns
```

## Example 2: Realistic - payment routing
```mermaid
classDiagram
    class PaymentOrder {
        +UUID orderId
        +String debtorIban
        +String creditorIban
        +submit() void
    }
    class Money {
        +Decimal value
        +String currency
    }
    class PaymentRoute {
        <<interface>>
        +route(order) Channel
    }
    class SepaRoute
    class SwiftRoute
    PaymentOrder *-- "1" Money : amount
    PaymentRoute <|.. SepaRoute
    PaymentRoute <|.. SwiftRoute
    PaymentOrder ..> PaymentRoute : uses
```

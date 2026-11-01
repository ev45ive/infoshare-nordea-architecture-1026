# Domain Model Diagram (DDD / UML-like)

Mermaid type: `classDiagram` (Native fit). Source: Modeling-Diagraming.md, section "Pipe, Pipe, pipe ... - Shared, Ubiqitous Language - Busines <> Code".

Represents business concepts, relationships, invariants, and shared vocabulary, answering what concepts exist in the problem domain and which distinctions matter to business rules.

## Example 1: Simple - Payment status

```mermaid
classDiagram
    class Payment {
        +PaymentId id
        +Money amount
        +PaymentStatus status
        +authorize()
        +settle()
    }
    class Money {
        +Decimal amount
        +String currency
    }
    class PaymentStatus {
        <<enumeration>>
        INITIATED
        AUTHORIZED
        SETTLED
        FAILED
    }
    Payment --> Money : amount
    Payment --> PaymentStatus : status
```

## Example 2: Realistic - Customer onboarding and accounts

```mermaid
classDiagram
    class Customer {
        +CustomerId id
        +String legalName
        +KycStatus kycStatus
        +Address registeredAddress
    }
    class Account {
        +AccountId id
        +IBAN iban
        +Money balance
        +AccountType type
        +debit(Money amount)
        +credit(Money amount)
    }
    class Money {
        +Decimal amount
        +Currency currency
    }
    class KycStatus {
        <<enumeration>>
        PENDING
        VERIFIED
        REJECTED
    }
    Customer "1" --> "0..*" Account : owns
    Account --> Money : balance
    Customer --> KycStatus : kycStatus
    note for Account "Balance never below overdraft limit"
```

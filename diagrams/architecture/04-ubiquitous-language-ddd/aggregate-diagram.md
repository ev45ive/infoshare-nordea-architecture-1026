# Aggregate Diagram (DDD)

Mermaid type: `classDiagram` (Close fit). Source: Modeling-Diagraming.md, section "Pipe, Pipe, pipe ... - Shared, Ubiqitous Language - Busines <> Code".

Shows aggregate roots, internal entities, value objects, and consistency boundaries, answering what must change atomically and where transactional invariants are enforced.

## Example 1: Simple - Card aggregate

```mermaid
classDiagram
    class Card {
        <<AggregateRoot>>
        +CardId id
        +CardStatus status
        +block()
        +unblock()
    }
    class CardLimit {
        <<ValueObject>>
        +Money dailyLimit
    }
    Card *-- CardLimit : limits
```

## Example 2: Realistic - Account with transaction journal

```mermaid
classDiagram
    class Account {
        <<AggregateRoot>>
        +AccountId id
        +IBAN iban
        +Money balance
        +post(Transaction tx)
    }
    class Transaction {
        <<Entity>>
        +TransactionId id
        +Money amount
        +DateTime bookedAt
    }
    class Money {
        <<ValueObject>>
        +Decimal amount
        +Currency currency
    }
    Account *-- "0..*" Transaction : journal
    Account *-- Money : balance
```

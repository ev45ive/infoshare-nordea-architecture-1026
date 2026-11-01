# Code Diagram (C4 Level 4)

Mermaid type: `classDiagram` (Close fit). Source: Modeling-Diagraming.md, section "System Context, Boundaries & Decomposition".

Describes implementation structures using classes, interfaces, and their relationships, showing how a component is implemented.

## Example 1: Simple - account hierarchy

```mermaid
classDiagram
    class Account {
        <<abstract>>
        +String iban
        +debit(Money amount) void
    }
    class SavingsAccount {
        +BigDecimal interestRate
        +accrueInterest() void
    }
    class CurrentAccount {
        +Money overdraftLimit
    }
    Account <|-- SavingsAccount
    Account <|-- CurrentAccount
```

## Example 2: Realistic - account repository with JDBC implementation

```mermaid
classDiagram
    class AccountRepository {
        <<interface>>
        +findByIban(String iban) Account
        +save(Account account) void
    }
    class JdbcAccountRepository {
        -DataSource dataSource
        +findByIban(String iban) Account
        +save(Account account) void
    }
    class Account {
        +String iban
    }
    class Money {
        +BigDecimal amount
        +String currency
    }
    AccountRepository <|.. JdbcAccountRepository
    JdbcAccountRepository ..> Account : maps rows to
    Account *-- Money : balance
```

# Profile Diagram (UML)

Mermaid type: `classDiagram` (Approximate fit). Source: Modeling-Diagraming.md, section "Software Structure, Object Models & Design".

The diagram answers how standard UML concepts can be customized consistently for a particular domain.

## Example 1: Simple - data sensitivity stereotypes
```mermaid
classDiagram
    class Customer {
        <<PII>>
        +String fullName
        +String personalId
        +String email
    }
    class Account {
        <<Audited>>
        +String iban
    }
    note for Customer "Tagged value: retention = 7 years"
    note for Account "Constraint: balance >= overdraft limit"
```

## Example 2: Realistic - aggregate root profile
```mermaid
classDiagram
    class UmlClass {
        <<metaclass>>
    }
    class AggregateRoot {
        <<stereotype>>
        +String consistencyScope
        +Boolean transactional
    }
    class Account {
        <<AggregateRoot>>
        +String iban
    }
    AggregateRoot --|> UmlClass : extends
    Account ..> AggregateRoot : stereotype applied
    note for Account "Tagged value: consistencyScope = AccountLedger"
```

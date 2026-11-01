# Component Diagram (UML)

Mermaid type: `classDiagram` with `<<interface>>` and `<<component>>` (Close fit). Source: Modeling-Diagraming.md, section "Boundaries & Decomposition".

Models components with provided and required interfaces and their dependency relationships, showing what contracts connect them.

## Example 1: Simple - payment service with two implementations

```mermaid
classDiagram
    class PaymentService {
        <<interface>>
        +submit(Payment payment) PaymentResult
    }
    class SepaPaymentService {
        +submit(Payment payment) PaymentResult
    }
    class InstantPaymentService {
        +submit(Payment payment) PaymentResult
    }
    PaymentService <|.. SepaPaymentService
    PaymentService <|.. InstantPaymentService
```

## Example 2: Realistic - replaceable fraud scoring component

```mermaid
classDiagram
    class CardAuthorization {
        <<component>>
    }
    class FraudScoring {
        <<interface>>
        +score(Transaction tx) RiskScore
    }
    class LedgerPort {
        <<interface>>
        +reserve(Money amount) ReservationId
    }
    class RulesBasedScorer {
        +score(Transaction tx) RiskScore
    }
    class MlScorer {
        +score(Transaction tx) RiskScore
    }
    CardAuthorization ..> FraudScoring : requires
    CardAuthorization ..> LedgerPort : requires
    RulesBasedScorer ..|> FraudScoring : provides
    MlScorer ..|> FraudScoring : provides
```

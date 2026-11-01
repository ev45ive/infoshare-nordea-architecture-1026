# API Contract / Interface Map

Mermaid type: `classDiagram` (Close fit). Source: Modeling-Diagraming.md, section "Integration, APIs & Distributed Systems".

Shows provided and consumed interfaces, endpoints, versions, and dependencies, answering what could break after a contract change.

## Example 1: Simple - Payments API versions and their consumers

```mermaid
classDiagram
    class PaymentsApiV1 {
        <<interface>>
        +createPayment(request) PaymentV1
        +getPayment(id) PaymentV1
    }
    class PaymentsApiV2 {
        <<interface>>
        +createPayment(request) PaymentV2
        +getPayment(id) PaymentV2
        +cancelPayment(id) PaymentV2
    }
    class MobileBankingApp
    class CorporateBankingPortal
    class LegacyCardGateway
    MobileBankingApp ..> PaymentsApiV2 : consumes
    CorporateBankingPortal ..> PaymentsApiV2 : consumes
    LegacyCardGateway ..> PaymentsApiV1 : consumes, deprecated
```

## Example 2: Realistic - Customer API v2 and v3 with dependent consumers

```mermaid
classDiagram
    class CustomerApiV2 {
        <<interface>>
        +getCustomer(customerId) CustomerDtoV2
    }
    class CustomerApiV3 {
        <<interface>>
        +getCustomer(customerId) CustomerDto
        +updateAddress(customerId, address) CustomerDto
        +listAccounts(customerId) AccountSummary
    }
    class OnboardingService
    class CrmSync
    class MobileBankingApp
    class RegulatoryReporting
    CustomerApiV2 --> CustomerApiV3 : successor
    OnboardingService ..> CustomerApiV3 : uses
    CrmSync ..> CustomerApiV3 : uses
    MobileBankingApp ..> CustomerApiV3 : uses
    RegulatoryReporting ..> CustomerApiV2 : uses, breaks if removed
```

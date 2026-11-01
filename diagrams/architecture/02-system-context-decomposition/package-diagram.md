# Package Diagram (UML)

Mermaid type: `classDiagram` with `namespace` (Close fit). Source: Modeling-Diagraming.md, section "Boundaries & Decomposition".

Shows logical packages, namespaces, modules, and the dependencies between them, including dependency cycles.

## Example 1: Simple - payments, accounts, reporting

```mermaid
classDiagram
    namespace Payments {
        class PaymentService
    }
    namespace Accounts {
        class AccountService
    }
    namespace Reporting {
        class ReportBuilder
    }
    PaymentService ..> AccountService : debits
    ReportBuilder ..> AccountService : reads
```

## Example 2: Realistic - module dependency cycle with shared kernel

```mermaid
classDiagram
    namespace Payments {
        class PaymentOrchestrator
        class SchemeGateway
    }
    namespace Accounts {
        class AccountService
    }
    namespace Reporting {
        class RegulatoryReportBuilder
    }
    namespace SharedKernel {
        class Money
        class Currency
    }
    PaymentOrchestrator ..> AccountService : debit and credit
    AccountService ..> PaymentOrchestrator : status callback
    PaymentOrchestrator ..> SchemeGateway
    RegulatoryReportBuilder ..> AccountService : reads balances
    PaymentOrchestrator ..> Money
    AccountService ..> Money
    Money *-- Currency
```

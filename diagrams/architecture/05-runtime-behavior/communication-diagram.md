# Communication Diagram (UML)

Mermaid type: `flowchart` (Approximate fit). Source: Modeling-Diagraming.md, section "Runtime Behavior, Interactions & State".

Emphasizes collaborating objects and their message relationships with ordering labels, answering which objects communicate and how responsibilities are distributed.

## Example 1: Simple - Loan approval collaboration
```mermaid
flowchart LR
    LA[LoanApplication] -- "1: submit()" --> VA[Validator]
    VA -- "2: checkIdentity()" --> KY[KycService]
    VA -- "3: scoreApplicant()" --> CS[CreditScorer]
    CS -- "4: getBureauReport()" --> BA[BureauAdapter]
    CS -- "5: score" --> VA
    VA -- "6: decide(limit)" --> DE[DecisionEngine]
```

## Example 2: Realistic - Card payment fraud check
```mermaid
flowchart TB
    PS[PaymentService] -- "1: authorize(txn)" --> FR[FraudRules]
    FR -- "2: score(txn)" --> ML[FraudModel]
    ML -- "3: riskScore" --> FR
    FR -- "4: limitCheck(card)" --> LS[LimitService]
    LS -- "5: ok" --> FR
    FR -- "6: decision" --> PS
    PS -- "7: postEntry(ledger)" --> LG[LedgerAdapter]
```

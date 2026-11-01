# Attack Tree

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Security, Privacy & Trust".

The diagram answers how an attacker could reach a specific outcome and which preventive or detective controls interrupt the attack.

## Example 1: Simple - Account takeover

```mermaid
flowchart TD
    Goal["Take over customer online banking account"]
    Goal -- "OR" --> Phish["Phish login credentials"]
    Goal -- "OR" --> Stuff["Credential stuffing with leaked passwords"]
    Goal -- "OR" --> SIM["SIM swap, then intercept SMS OTP"]
    Phish --> C1{{"Control: phishing-resistant MFA"}}
    Stuff --> C2{{"Control: breached-password check"}}
    SIM --> C3{{"Control: SIM-change hold and alert"}}
```

## Example 2: Realistic - Altering a payment amount after approval

```mermaid
flowchart TD
    Goal["Alter payment amount after approval"]
    Goal -- "AND" --> Intercept["Modify request in transit"]
    Goal -- "AND" --> Bypass["Pass integrity check"]
    Intercept -- "OR" --> MITM["Man-in-the-middle on internal link"]
    Intercept -- "OR" --> Svc["Compromise payment-init service account"]
    Bypass --> Forge["Forge message signature"]
    MITM --> C1{{"Control: mTLS with certificate pinning"}}
    Svc --> C2{{"Control: short-lived vault secrets"}}
    Forge --> C3{{"Control: ledger verifies signature, not gateway"}}
    Goal -.-> C4{{"Detective: dual approval above 10,000 EUR"}}
```

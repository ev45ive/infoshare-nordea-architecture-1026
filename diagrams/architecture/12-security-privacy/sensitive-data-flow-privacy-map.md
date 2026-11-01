# Sensitive Data Flow / Privacy Map

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Security, Privacy & Trust".

The diagram answers where sensitive information is processed, who can access it, and which privacy obligations and exposure risks exist.

## Example 1: Simple - Customer PII from onboarding to analytics

```mermaid
flowchart LR
    classDef pii fill:#fde2e2,stroke:#b42318
    classDef store fill:#e3f1e3,stroke:#1d6b2f
    Onboarding["Onboarding service"]:::pii
    Crm[("CRM customer master")]:::store
    Pseudo["Pseudonymization job"]
    Analytics[("Analytics warehouse")]:::store
    Onboarding -- "Name, national ID, address" --> Crm
    Crm -- "Name, national ID, address" --> Pseudo
    Pseudo -- "Hashed customer key only" --> Analytics
```

## Example 2: Realistic - Card number tokenized before logging, credit bureau check

```mermaid
flowchart LR
    classDef pii fill:#fde2e2,stroke:#b42318
    classDef safe fill:#e3f1e3,stroke:#1d6b2f
    classDef ext fill:#fef0c7,stroke:#b54708
    CardEntry["Card entry, PAN"]:::pii
    Token["Tokenization service"]:::safe
    Logs[("Application logs, token only")]:::safe
    Loan["Loan decisioning"]:::pii
    Bureau["External credit bureau"]:::ext
    CardEntry -- "PAN over TLS" --> Token
    Token -- "Token only" --> Logs
    Token -- "Token reference" --> Loan
    Loan -- "National ID and income, with consent" --> Bureau
```

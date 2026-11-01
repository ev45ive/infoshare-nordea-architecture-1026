# Threat Modeling DFD

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Security, Privacy & Trust".

The diagram answers what can be attacked and where spoofing, tampering, information disclosure, or privilege escalation could occur.

## Example 1: Simple - Login flow with spoofing risk

```mermaid
flowchart LR
    classDef untrusted fill:#fde2e2,stroke:#b42318
    classDef trusted fill:#e3f1e3,stroke:#1d6b2f
    Customer((Customer)):::untrusted
    Login[P1 Login service]:::trusted
    Credentials[(D1 Credential store)]:::trusted
    Customer -- "F1 credentials [S: spoofing]" --> Login
    Login -- "F2 hash lookup [T: tampering]" --> Credentials
    Login -- "F3 session token [I: disclosure]" --> Customer
```

## Example 2: Realistic - Back-office admin API with privilege escalation

```mermaid
flowchart TB
    classDef untrusted fill:#fde2e2,stroke:#b42318
    classDef dmz fill:#fef0c7,stroke:#b54708
    classDef trusted fill:#e3f1e3,stroke:#1d6b2f
    Operator((Back-office operator)):::untrusted
    AdminAPI[P2 Admin API]:::dmz
    Entitlements[P3 Entitlement service]:::trusted
    Ledger[(D2 Customer ledger)]:::trusted
    AuditLog[(D3 Audit log, append-only)]:::trusted
    Operator -- "F1 admin request [S: spoofed operator]" --> AdminAPI
    AdminAPI -- "F2 role check [E: privilege escalation]" --> Entitlements
    AdminAPI -- "F3 adjust balance [T: tampering]" --> Ledger
    Ledger -- "F4 change event [R: repudiation]" --> AuditLog
```

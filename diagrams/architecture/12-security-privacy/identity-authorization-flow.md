# Identity & Authorization Flow Diagram

Mermaid type: `sequenceDiagram` (Native fit). Source: Modeling-Diagraming.md, section "Security, Privacy & Trust".

The diagram answers who authenticates whom, where permissions are enforced, and how identities and credentials flow through the system.

## Example 1: Simple - Mobile banking login with OAuth2 authorization code and PKCE

```mermaid
sequenceDiagram
    actor Customer
    participant App as Mobile banking app
    participant IdP as Nordea identity provider
    participant API as Accounts API
    Customer->>App: Open app and tap log in
    App->>IdP: Authorization request with PKCE challenge
    IdP->>Customer: Login page, password and BankID approval
    Customer->>IdP: Credentials and approval
    IdP-->>App: Authorization code
    App->>IdP: Code and PKCE verifier
    IdP-->>App: Short-lived access token and refresh token
    App->>API: GET /accounts with Bearer token
    API->>API: Verify signature and scope accounts:read
    API-->>App: Account list
```

## Example 2: Realistic - Service-to-service token exchange with policy check

```mermaid
sequenceDiagram
    participant Svc as Payments service
    participant STS as Token service
    participant Ledger as Core ledger API
    participant PDP as Policy decision point
    Svc->>STS: Token exchange with workload identity (RFC 8693)
    STS->>STS: Validate workload certificate and namespace
    STS-->>Svc: Token with audience ledger, 5 minute TTL
    Svc->>Ledger: POST /postings with Bearer token
    Ledger->>PDP: May payments-svc post with postings:write?
    alt Permit
        PDP-->>Ledger: Permit, amount under 50,000 EUR
        Ledger-->>Svc: 201 Created
    else Deny
        PDP-->>Ledger: Deny
        Ledger-->>Svc: 403 Forbidden, audit event logged
    end
```

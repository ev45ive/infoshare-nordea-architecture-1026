# Component Diagram (C4 Level 3)

Mermaid type: `C4Component` (Native fit). Source: Modeling-Diagraming.md, section "System Context, Boundaries & Decomposition".

Shows the major logical components inside a particular application or service, and how they interface and depend on each other.

## Example 1: Simple - payment service

```mermaid
C4Component
    title Payment service - components
    Container_Boundary(pay, "Payment service") {
        Component(val, "Payment validator", "Java", "Checks format, limits, and sanctions flags")
        Component(router, "Payment router", "Java", "Selects SEPA or domestic rail")
        Component(ledger, "Ledger adapter", "Java", "Posts entries to core ledger")
    }
    System_Ext(core, "Core banking", "Ledger system")
    System_Ext(sepa, "SEPA gateway", "Clearing")
    Rel(val, router, "Passes valid payment")
    Rel(router, ledger, "Requests posting")
    Rel(router, sepa, "Submits SEPA payment", "ISO 20022")
    Rel(ledger, core, "Posts entries", "REST")
```

## Example 2: Realistic - authentication service

```mermaid
C4Component
    title Authentication service - components
    Container_Boundary(auth, "Authentication service") {
        Component(login, "Login controller", "Spring MVC", "Handles credentials and MFA steps")
        Component(issuer, "Token issuer", "Spring Security", "Issues OAuth2 access tokens")
        Component(store, "User store adapter", "LDAP client", "Reads customer credentials")
    }
    System_Ext(ldap, "Customer directory", "LDAP")
    System_Ext(mfa, "MFA provider", "One-time codes")
    Rel(login, mfa, "Verifies one-time code")
    Rel(login, issuer, "Requests token")
    Rel(login, store, "Loads user")
    Rel(store, ldap, "Queries", "LDAPS")
```

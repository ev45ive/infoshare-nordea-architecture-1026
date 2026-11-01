# System Landscape Diagram (C4)

Mermaid type: `C4Context` (Native fit). Source: Modeling-Diagraming.md, section "System Context, Boundaries & Decomposition".

Shows which software systems exist across the organization, how they depend on each other, and where responsibilities overlap.

## Example 1: Simple - bank systems

```mermaid
C4Context
    title Bank system landscape
    System(crm, "CRM", "Customer profiles and cases")
    System(core, "Core banking", "Accounts and ledger")
    System(cards, "Card management", "Card lifecycle and limits")
    System(dwh, "Data platform", "Analytics and reporting")
    Rel(crm, core, "Reads customer accounts")
    Rel(cards, core, "Posts card transactions")
    Rel(core, dwh, "Exports daily ledger")
```

## Example 2: Realistic - overlapping customer address ownership

```mermaid
C4Context
    title Customer address ownership
    System(crm, "CRM", "Sales and service view of customers")
    System(kyc, "KYC platform", "Identity verification and address checks")
    System(core, "Core banking", "Customer master data")
    System(onb, "Onboarding portal", "Digital account opening")
    Rel(onb, kyc, "Verifies identity and address")
    Rel(onb, core, "Creates customer record")
    Rel(crm, core, "Syncs customer address")
    Rel(kyc, core, "Updates verified address")
```

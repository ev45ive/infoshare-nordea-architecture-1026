# Customer Journey Map

Mermaid type: `journey` (Native fit). Source: Modeling-Diagraming.md, section "Business Processes, Workflows & Decisions".

It answers what the customer experiences across channels and where organizational or system boundaries harm that experience.

## Example 1: Simple - Opening a current account across app and branch

```mermaid
journey
    title Opening a current account
    section Discover
      Sees offer in mobile app: 4: Customer
      Starts application online: 3: Customer, Mobile app
    section Verify
      Uploads ID documents: 2: Customer, Onboarding service
      Waits for manual review: 1: Customer, Back office
    section Activate
      Visits branch to collect card: 3: Customer, Branch
```

## Example 2: Realistic - Replacing a lost debit card

```mermaid
journey
    title Replacing a lost debit card
    section Report
      Blocks card in mobile app: 5: Customer, Mobile app
      Calls contact centre to confirm: 2: Customer, Contact centre
    section Replace
      Waits for new card by post: 2: Customer, Card operations
      PIN mailer arrives a week later: 1: Customer, Card operations
    section Resume
      Sets new PIN in app: 4: Customer, Mobile app
      Retries pending payments: 3: Customer, Payments
```

# Capability Map (ArchiMate)

Mermaid type: `mindmap` (Close fit). Source: Modeling-Diagraming.md, section "Enterprise Architecture & Business Strategy".

Shows what the organization must be able to do, independent of its structure, and which capabilities are missing, duplicated, weak, or strategically important.

## Example 1: Simple - L1/L2 capability tree

```mermaid
mindmap
  root((Retail Bank))
    Payments
      Domestic transfers
      Card authorization
      Instant payments
    Customer
      Onboarding
      KYC screening
    Core Banking
      Account management
      Ledger posting
    Regulatory Reporting
      Supervisory reporting
      AML monitoring
```

## Example 2: Realistic - duplicated and weak capabilities

```mermaid
mindmap
  root((Retail Banking Capabilities))
    Payments
      Card dispute handling - duplicated in two units
      Payment routing - weak maturity
    Customer Servicing
      Complaint management - weak maturity
      Identity verification
    Risk and Compliance
      Fraud detection - strategic priority
      AML monitoring
    Data
      Regulatory reporting
      Customer master data - duplicated across CRM and core
```

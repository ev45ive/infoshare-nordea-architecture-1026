# Change Impact Diagram

Mermaid type: `mindmap` (Close fit). Source: Modeling-Diagraming.md, section "Architecture Evolution, Migration & Planning".

Maps a proposed change to affected services, interfaces, data stores, business processes, and stakeholders, answering what else may break or need modification and who must coordinate or approve the change.

## Example 1: Simple - Customer ID format change

```mermaid
mindmap
  root((Customer ID format change))
    Services
      Onboarding service
      Card service
    Interfaces
      Core banking API v3
      Batch file to regulator
    Data stores
      CRM master table
      Data warehouse
    Processes
      KYC refresh
    Stakeholders
      Data governance board
      Regulatory reporting team
```

## Example 2: Realistic - New account field

```mermaid
mindmap
  root((New account field: IBAN status))
    Services
      Account service
      Payment initiation
    Interfaces
      Open banking API v2
      Mobile app API
    Data stores
      Account DB
      Reporting mart
    Processes
      Monthly regulatory report
      Customer statement run
    Stakeholders
      Product owner
      Architecture board
```

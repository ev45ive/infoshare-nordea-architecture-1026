# Sequence Diagram (UML)

Mermaid type: `sequenceDiagram` (Native fit). Source: Modeling-Diagraming.md, section "Runtime Behavior, Interactions & State".

Shows messages exchanged between participants in chronological order, answering who calls whom and where retries, timeouts, and failures occur.

## Example 1: Simple - Card payment authorization
```mermaid
sequenceDiagram
    participant M as Merchant POS
    participant G as Payment Gateway
    participant A as Authorization Service
    participant I as Card Issuer
    M->>G: Authorize 42.50 EUR
    G->>A: POST /authorizations
    A->>I: ISO 8583 0100 request
    alt Approved
        I-->>A: 0110 response code 00
        A-->>G: APPROVED
        G-->>M: Approved
    else Issuer timeout
        A-->>G: DECLINED, timeout
        G-->>M: Declined, retry later
    end
```

## Example 2: Realistic - SEPA transfer with timeout and retry
```mermaid
sequenceDiagram
    participant App as Mobile Banking
    participant TS as Transfer Service
    participant CL as Core Ledger
    participant SP as SEPA Gateway
    App->>TS: POST /transfers (Idempotency-Key)
    TS->>CL: Debit source account
    CL-->>TS: 200 OK
    TS->>SP: Submit pain.001 credit transfer
    Note over TS,SP: No response within 5 s
    loop Up to 3 status inquiries
        TS->>SP: Status inquiry (same key)
    end
    alt Settled
        SP-->>TS: ACSC
        TS-->>App: 201 Completed
    else Rejected
        SP-->>TS: RJCT
        TS->>CL: Reverse debit
        TS-->>App: 422 Rejected
    else Still pending after retries
        TS-->>App: 202 Pending confirmation
    end
```

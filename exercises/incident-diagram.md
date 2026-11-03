# Incident: duplicate authorization and unbalanced AR (order o_900771)

Source: [incident.logs](./incident.logs). Period: 2026-03-02 09:58 to 2026-03-03 08:10.

Mermaid type: `sequenceDiagram` for the timeline, `flowchart` for the causal chain.

## Timeline

```mermaid
sequenceDiagram
    autonumber
    participant Cust as Customer
    participant GW as api-gw
    participant ORD as order-svc
    participant PAY as payment-svc
    participant STR as Stripe
    participant ADY as Adyen
    participant INV as invoicing-svc
    participant LED as ledger-svc
    participant OPS as Ops and jobs

    rect rgb(230, 245, 230)
    Note over Cust,OPS: 09:58 Checkout, confirm, capture (happy path)
    Cust->>GW: POST /checkout
    GW->>ORD: CreateCheckout
    ORD->>ORD: Order o_900771 DRAFT 189.64 EUR
    ORD-)PAY: OrderDrafted (orders topic)
    PAY->>STR: CreatePaymentIntent 18964 key pay:o_900771:2026-03-02
    STR-->>PAY: pi_3PzN7eK9 requires_payment_method
    Cust->>GW: POST /checkout/confirm
    ORD->>ORD: PENDING_PAYMENT
    STR-)PAY: Webhook payment_intent.succeeded
    PAY->>PAY: Record p_450991 AUTHORIZED
    PAY-)ORD: PaymentAuthorized seq 1
    ORD->>ORD: CONFIRMED
    ORD-)INV: OrderConfirmed
    INV->>LED: Invoice INV 882100 issued 189.64
    LED->>LED: Journal j_90110 posted
    PAY->>STR: Capture pi_3PzN7eK9 18964
    STR-->>PAY: ch_1Qw9xA captured
    PAY-)ORD: PaymentCaptured seq 2
    ORD->>ORD: PAID, fulfillment ships
    end

    rect rgb(255, 243, 220)
    Note over Cust,OPS: 10:03 Add SKU-GAMMA after payment (amendment, +27.62 EUR)
    Cust->>GW: POST /orders/o_900771/amend
    GW->>ORD: AmendOrder total 217.26
    ORD->>PAY: Start payment for amendment delta 2762
    PAY->>STR: CreatePaymentIntent key pay:o_900771:2026-03-02 same key
    STR-->>PAY: Idempotent replay returns pi_3PzN7eK9
    Note over PAY: Delta gets no new intent
    ORD->>INV: Amendment invoice INV 882155 27.62
    INV->>LED: InvoiceIssued type AMENDMENT
    PAY->>STR: Capture 2762 on pi_3PzN7eK9
    STR-->>PAY: ERROR amount_exceeds_authorized
    ORD->>ORD: Amendment payment failed, action fallback_reauth
    end

    rect rgb(255, 230, 230)
    Note over Cust,OPS: 10:04 Fallback to Adyen in GBP
    PAY->>ADY: FX EUR to GBP 0.8571, intent 23.67 GBP
    ADY-->>PAY: ady_pi_77219 authorized
    PAY->>ADY: Capture 23.67 GBP
    ADY-->>PAY: psp_889120 captured
    PAY-)ORD: PaymentCaptured p_451020 seq 3
    ORD->>ORD: OrderAmended seq 2
    LED->>LED: Journal j_90188 AR 27.62 EUR
    end

    rect rgb(230, 230, 255)
    Note over Cust,OPS: 11:30 to 12:06 Reconciliation, support retry, duplicate webhook
    Note over OPS: 11:30 Recon mismatch -0.01 EUR, case LOW
    OPS->>PAY: 12:05 playbook retry_failed_capture on pi_3PzN7eK9
    PAY->>STR: Capture 2762 EUR
    STR-->>PAY: ERROR charge_already_captured
    PAY->>STR: Create intent manual, same key
    STR-->>PAY: Replay pi_3PzN7eK9, no new intent
    STR-)PAY: 12:06 Webhook duplicate attempt 2
    PAY->>PAY: Dedup MISS, upsert matches p_450991, no new row
    PAY-)ORD: PaymentAuthorized seq 4
    ORD->>ORD: Idempotency guard HIT, skip
    PAY-)LED: PaymentAuthorized p_450991
    LED->>LED: Key order, event, day MISS, posts j_90241 AR 189.64
    end

    rect rgb(240, 240, 240)
    Note over Cust,OPS: 23:59 Close and next-day reversal
    Note over OPS: 23:59 Daily close, AR unbalanced +189.64 EUR, MEDIUM
    OPS->>LED: 03-03 08:10 Manual reversal of duplicate auth, same weak key
    LED->>LED: Reversal j_90302 reverses j_90241
    Note over LED: ar_aging and dso may already include j_90241
    end
```

## Causal chain

```mermaid
flowchart LR
    subgraph Payments
        A["Idempotency key orderId plus utcDate reused for amendment and retry"]
        B["Stripe replays pi_3PzN7eK9, no new intent"]
        C["Capture of delta fails amount_exceeds_authorized"]
        D["Fallback to Adyen in GBP, FX rounding diff"]
        E["Webhook duplicate, dedup MISS, PaymentAuthorized seq 4 re-emitted"]
    end

    subgraph Ledger
        F["Weak key order, event, day"]
        G["Second PAYMENT_AUTH journal j_90241 for 189.64"]
    end

    H["Close: AR unbalanced"]
    I["Reversal by same weak key may hit materialized views"]

    A --> B
    B --> C
    C --> D
    B --> E
    E --> F
    F --> G
    G --> H
    H --> I
```

## Legend

| Term | Meaning |
|---|---|
| `pi_3PzN7eK9` | Stripe PaymentIntent for order o_900771 (189.64 EUR) |
| `p_450991` | Internal payment record for the authorization |
| `p_451020` | Internal payment record for the Adyen fallback capture |
| `j_90110`, `j_90188`, `j_90241`, `j_90302` | Ledger journals: original, amendment, duplicate auth, reversal |
| `seq` | Sequence number on the event |

## Notes

- Amounts are in EUR unless marked GBP. Times are local (+01:00).
- The amendment delta (27.62 EUR) was never charged on its own intent. The reused key made Stripe return the original intent, so the fallback to Adyen was needed.
- The duplicate authorization is booked in the ledger, not in payments. Payments upserted the same row, but the ledger's weaker key let it post again.
- Customer contact data and card identifiers from the log are left out of the diagram.

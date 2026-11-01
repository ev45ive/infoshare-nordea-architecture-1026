# Trust Boundary Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Security, Privacy & Trust".

The diagram answers where untrusted input enters and which interactions require authentication, validation, or other controls.

## Example 1: Simple - Internet to core zone

```mermaid
flowchart LR
    subgraph Internet["Untrusted: Internet"]
        Customer[Customer browser]
    end
    subgraph DMZ["Semi-trusted: DMZ"]
        WAF[Web application firewall]
        Gateway[API gateway]
    end
    subgraph Core["Trusted: core zone"]
        Payments[Payments service]
        Ledger[(Core ledger DB)]
    end
    Customer -- "HTTPS, OAuth2 token" --> WAF
    WAF --> Gateway
    Gateway -- "mTLS, schema-validated payload" --> Payments
    Payments -- "TLS, least-privilege DB account" --> Ledger
```

## Example 2: Realistic - Card scheme callback across a partner boundary

```mermaid
flowchart LR
    subgraph Scheme["Untrusted: card scheme and merchants"]
        Callback[Card scheme callback]
    end
    subgraph Edge["Boundary 1: DMZ"]
        Receiver[Callback receiver]
    end
    subgraph Payments["Boundary 2: payments zone"]
        Auth[Authorization service]
        Vault[(Card token vault)]
    end
    Callback -- "Signed message, IP allow-list" --> Receiver
    Receiver -- "Replay check, message validation" --> Auth
    Auth -- "Tokenized card number only" --> Vault
```

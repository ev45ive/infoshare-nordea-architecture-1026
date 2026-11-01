# Security Zone / Segmentation Diagram

Mermaid type: `block-beta` (Close fit). Source: Modeling-Diagraming.md, section "Security, Privacy & Trust".

The diagram answers which assets must be isolated and where firewalls, gateways, and access restrictions should be enforced.

## Example 1: Simple - Public, internal, and restricted zones

```mermaid
block-beta
    columns 3
    PublicLabel["Public zone: internet-facing"]:3
    block:PublicZone:3
        columns 3
        CDN["CDN"]
        WAF["WAF"]
        Portal["Online banking portal"]
    end
    InternalLabel["Internal zone: services"]:3
    block:InternalZone:3
        columns 3
        Payments["Payments API"]
        Accounts["Accounts service"]
        Fraud["Fraud scoring"]
    end
    RestrictedLabel["Restricted zone: PCI and core"]:3
    block:RestrictedZone:3
        columns 2
        Vault["Card token vault"]
        Core["Core banking DB"]
    end
    PublicZone --> InternalZone
    InternalZone --> RestrictedZone
```

## Example 2: Realistic - PCI zone reachable only through an integration gateway

```mermaid
block-beta
    columns 3
    MktLabel["Marketing zone: no card data"]:3
    block:MarketingZone:3
        columns 3
        Crm["CRM"]
        Campaigns["Campaign engine"]
        Analytics["Web analytics"]
    end
    IntegrationLabel["Integration zone: gateways"]:3
    block:IntegrationZone:3
        columns 1
        TokenGw["Tokenization gateway, mTLS only"]
    end
    CardLabel["PCI zone: isolated"]:3
    block:CardZone:3
        columns 2
        Tokenizer["PCI tokenizer"]
        CardVault["Card vault"]
    end
    MarketingZone --> IntegrationZone
    IntegrationZone --> CardZone
```

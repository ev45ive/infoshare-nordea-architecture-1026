# Network Topology Diagram

Mermaid type: `flowchart` (Close fit). Source: Modeling-Diagraming.md, section "Infrastructure, Deployment & Network Architecture".

Shows networks, subnets, routers, firewalls, gateways, and connections.

## Example 1: Simple - internet ingress through DMZ into application and data zones

```mermaid
flowchart LR
    internet((Internet)) -->|HTTPS 443| fw1[[Perimeter Firewall]]
    fw1 --> waf
    subgraph DMZ ["DMZ 10.10.0.0/24"]
        waf[WAF and Load Balancer]
    end
    waf -->|HTTPS 8443| fw2[[Internal Firewall]]
    fw2 --> app
    subgraph APP ["Application Zone 10.20.0.0/24"]
        app[Payments API]
    end
    app -->|SQL 5432| fw3[[Data Firewall]]
    fw3 --> db
    subgraph DATA ["Data Zone 10.30.0.0/24"]
        db[(Payments DB)]
    end
```

## Example 2: Realistic - branch ATM network over IPsec into PCI and core zones

```mermaid
flowchart TB
    subgraph BRANCH ["Branch Office"]
        atm[ATM Network]
    end
    subgraph DC ["Head Office Data Center"]
        vpn{{IPsec VPN Gateway}}
        fw[[Segmentation Firewall]]
        subgraph PCI ["PCI Zone 10.40.0.0/24"]
            card[Card Switch]
        end
        subgraph CORE ["Core Zone 10.50.0.0/24"]
            ledger[(Core Ledger)]
        end
    end
    atm -->|IPsec tunnel| vpn
    vpn -->|allow 443 only| fw
    fw --> card
    card -->|ISO 8583 over MQ| ledger
    fw -.->|direct DB access blocked| ledger
```

# Infrastructure Topology Diagram

Mermaid type: `architecture-beta` (Close fit). Source: Modeling-Diagraming.md, section "Infrastructure, Deployment & Network Architecture".

Shows servers, load balancers, databases, storage, networking, and supporting infrastructure.

## Example 1: Simple - load balancer, two app servers, database

```mermaid
architecture-beta
    group dc(cloud)[Data Center]
    service lb(internet)[Load Balancer] in dc
    service app1(server)[App Server 1] in dc
    service app2(server)[App Server 2] in dc
    service db(database)[Payments DB] in dc
    service bak(disk)[Backup Storage] in dc
    lb:R --> L:app1
    lb:R --> L:app2
    app1:B --> T:db
    app2:B --> T:db
    db:R --> L:bak
```

## Example 2: Realistic - payments platform with HA database and monitoring

```mermaid
architecture-beta
    group dc(cloud)[Payments Data Center]
    group mon(cloud)[Monitoring]
    service edge(internet)[Edge Load Balancer] in dc
    service api1(server)[Payments API 1] in dc
    service api2(server)[Payments API 2] in dc
    service pdb(database)[Ledger DB Primary] in dc
    service sdb(database)[Ledger DB Standby] in dc
    service san(disk)[SAN Storage] in dc
    service prom(server)[Metrics Server] in mon
    edge:R --> L:api1
    edge:R --> L:api2
    api1:B --> T:pdb
    api2:B --> T:pdb
    pdb:R --> L:sdb
    pdb:B --> T:san
    api1:R --> L:prom
```

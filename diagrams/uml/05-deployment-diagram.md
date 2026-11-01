# Deployment diagram

Mermaid type: `flowchart` (Approximate fit). UML type: deployment diagram.

Mermaid has no deployment diagram. Nodes and execution environments are drawn as subgraphs, and deployed artifacts as nodes inside them.

## Description

Mapping of software artifacts onto hardware nodes and execution environments, including the communication paths between them.

## Example usages

- Infrastructure topology for cloud or on-premises systems
- Showing which artifact runs on which node or container
- Documenting network protocols and ports between nodes
- Comparing environments (dev, test, prod)

## Example 1: Simple - API and database on separate nodes

```mermaid
flowchart TB
    subgraph server["App server (node)"]
        app["Orders API artifact"]
    end
    subgraph dbnode["DB server (node)"]
        db[("Orders DB")]
    end
    app -->|JDBC| db
```

## Example 2: Complex - Containerized API with managed database

```mermaid
flowchart TB
    gw["API gateway"]
    subgraph aks["AKS cluster (execution environment)"]
        subgraph pod["Pod"]
            api["orders-api.jar"]
        end
    end
    subgraph paas["Azure SQL (managed node)"]
        db[("Orders DB")]
    end
    gw -->|HTTPS| api
    api -->|TLS 1433| db
```

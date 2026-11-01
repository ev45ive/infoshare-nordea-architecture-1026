# Layered viewpoint

ArchiMate viewpoint: Layered. Mermaid type: `flowchart` (Close fit).

Business, application, and technology layers are drawn as subgraphs. Cross-layer relationships are shown as labeled edges.

## Description

Shows the business, application, and technology layers together, with the services that cross from one layer to the next.

## Example usages

- Giving an overview of the full architecture on one page
- Showing which technology supports which application service
- Explaining cross-layer dependencies to stakeholders
- Checking that every business process is supported by an application

## Example 1: Simple - Process supported by application and database

```mermaid
flowchart TB
    subgraph biz["Business layer"]
        process["Order process"]
    end
    subgraph app["Application layer"]
        orderApp["Order application"]
    end
    subgraph tech["Technology layer"]
        db[("Database")]
    end
    process -.-> orderApp
    orderApp -.-> db
```

## Example 2: Complex - Full stack for order handling

```mermaid
flowchart TB
    subgraph biz["Business layer"]
        process["Order process"]
        customer["Customer role"]
    end
    subgraph app["Application layer"]
        portal["Web portal"]
        orderApp["Order application"]
        dataSvc["Data service"]
    end
    subgraph tech["Technology layer"]
        vm["Kubernetes cluster"]
        db[("Database")]
    end
    customer --> process
    process -.->|served by| portal
    portal --> orderApp
    orderApp --> dataSvc
    dataSvc -.->|runs on| vm
    dataSvc --> db
```

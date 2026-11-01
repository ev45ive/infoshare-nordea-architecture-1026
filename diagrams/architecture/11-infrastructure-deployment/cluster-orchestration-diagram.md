# Cluster / Orchestration Diagram

Mermaid type: `flowchart` (Approximate fit). Source: Modeling-Diagraming.md, section "Infrastructure, Deployment & Network Architecture".

Shows Kubernetes clusters or equivalent orchestration structures, workloads, services, ingress, and scaling groups.

## Example 1: Simple - ingress to a service and its deployments in one namespace

```mermaid
flowchart TB
    user([Users]) --> ing["Ingress Controller"]
    subgraph ns ["Namespace: payments"]
        svc["Service payments-api"]
        dep1["Deployment payments-api (3 replicas)"]
        dep2["Deployment payment-worker (2 replicas)"]
        svc --> dep1
        dep1 --> dep2
    end
    ing --> svc
```

## Example 2: Realistic - node pools with autoscaling for API and fraud workloads

```mermaid
flowchart TB
    traffic([Ingress Traffic]) --> ingress["Ingress Controller (HA)"]
    subgraph cluster ["Production Cluster EU-North"]
        subgraph poolA ["Node pool: general (autoscale 3-12)"]
            gw["api-gateway pods"]
            api["payments-api pods"]
        end
        subgraph poolB ["Node pool: memory (autoscale 2-6)"]
            fraud["fraud-scoring pods"]
        end
        hpa{{"HPA on CPU and queue depth"}}
    end
    ingress --> gw
    gw --> api
    api --> fraud
    hpa -.->|scales| api
```

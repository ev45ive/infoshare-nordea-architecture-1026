# Deployment Diagram (UML / C4 variants)

Mermaid type: `C4Deployment` (Native fit). Source: Modeling-Diagraming.md, section "Infrastructure, Deployment & Network Architecture".

Maps software artifacts, services, and containers onto execution environments and infrastructure nodes.

## Example 1: Simple - API on Kubernetes, database on VM

```mermaid
C4Deployment
    title Payments API deployment
    Deployment_Node(k8s, "Kubernetes Cluster", "OpenShift, Nordic DC") {
        Container(api, "Payments API", "Java / Spring Boot", "Accepts payment orders")
    }
    Deployment_Node(vm, "Database VM", "RHEL 9") {
        ContainerDb(db, "Payments DB", "PostgreSQL 16", "Stores payment orders")
    }
    Rel(api, db, "Reads and writes", "JDBC over TLS")
```

## Example 2: Realistic - card authorization across on-premise and private cloud

```mermaid
C4Deployment
    title Card authorization deployment
    Deployment_Node(dc, "Nordic Data Center", "On-premise") {
        Deployment_Node(mf, "Core Banking Host", "Linux VM") {
            ContainerDb(core, "Core Ledger", "Oracle 19c", "Account balances and postings")
        }
    }
    Deployment_Node(cloud, "Private Cloud Region", "EU") {
        Deployment_Node(ocp, "Kubernetes Cluster", "OpenShift") {
            Container(auth, "Card Authorization", "Java 21", "Approves or declines card transactions")
            Container(fraud, "Fraud Scoring", "Python / ONNX", "Scores transactions in real time")
        }
    }
    Rel(auth, fraud, "Requests score", "gRPC over mTLS")
    Rel(auth, core, "Reserves funds", "MQ over TLS")
```

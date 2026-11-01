# Container Diagram (C4 Level 2)

Mermaid type: `C4Container` (Native fit). Source: Modeling-Diagraming.md, section "System Context, Boundaries & Decomposition".

Decomposes a system into applications, services, databases, and other runnable or storage units.

## Example 1: Simple - payment initiation

```mermaid
C4Container
    title Payment initiation - containers
    Person(customer, "Customer", "Initiates transfers")
    System_Boundary(pay, "Payment initiation") {
        Container(web, "Web app", "React", "Transfer screens")
        Container(api, "Payments API", "Java, Spring Boot", "Validates and routes payments")
        ContainerDb(db, "Payments DB", "PostgreSQL", "Payment status and history")
        ContainerQueue(q, "Payment events", "Kafka", "Payment status events")
    }
    System_Ext(core, "Core banking", "Ledger")
    Rel(customer, web, "Uses", "HTTPS")
    Rel(web, api, "Calls", "JSON/HTTPS")
    Rel(api, db, "Reads and writes", "JDBC")
    Rel(api, q, "Publishes", "Kafka")
    Rel(api, core, "Posts entries", "REST")
```

## Example 2: Realistic - regulatory reporting

```mermaid
C4Container
    title Regulatory reporting - containers
    System_Ext(ledger, "Core banking", "Source ledger")
    System_Ext(regp, "Regulator portal", "Receives report files")
    System_Boundary(reg, "Regulatory reporting") {
        Container(sched, "Scheduler", "Kubernetes CronJob", "Starts nightly run")
        ContainerQueue(q, "Job queue", "RabbitMQ", "Report tasks")
        Container(worker, "Report worker", "Python", "Builds COREP and FINREP files")
        ContainerDb(stage, "Staging store", "PostgreSQL", "Validated ledger extracts")
    }
    Rel(sched, q, "Enqueues jobs")
    Rel(q, worker, "Delivers jobs")
    Rel(worker, ledger, "Extracts balances", "SFTP")
    Rel(worker, stage, "Stores extracts", "JDBC")
    Rel(worker, regp, "Submits files", "HTTPS")
```

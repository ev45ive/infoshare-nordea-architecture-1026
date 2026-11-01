# Mermaid Alternatives for Modeling Diagram Types

Maps each diagram type from [Modeling-Diagraming.md](../Modeling-Diagraming.md) to the closest Mermaid type, with simple realistic example ideas.

## Fit legend

- **Native**: Mermaid has a diagram type for this notation.
- **Close**: a Mermaid type covers most of the notation with minor adaptation.
- **Approximate**: no matching type; a flowchart or block diagram with styling stands in.

Notes: Mermaid has no ArchiMate, UML use case, BPMN, or object diagram types. `architecture-beta`, `block-beta`, and `radar-beta` are newer and may need a recent Mermaid version.

## Enterprise Architecture & Business Strategy

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Capability Map | mindmap (L1/L2 hierarchy) or block-beta (grid) | Close | 1) Retail bank L1/L2 capability tree<br>2) Capability heatmap colored by maturity<br>3) Payments capability duplicated across two units |
| Business Motivation Diagram | flowchart TD for drivers, goals, requirements (requirementDiagram for requirements) | Close | 1) PSD2 regulation driving an open-API goal<br>2) Cost-reduction driver linked to cloud migration goal<br>3) "Batch reporting too slow" assessment linked to a requirement |
| Stakeholder Viewpoint | quadrantChart (influence vs interest) | Close | 1) Mortgage system stakeholders plotted by influence and interest<br>2) Compliance officer: high influence, low interest<br>3) Branch managers: high interest, low influence |
| Goal Realization Diagram | flowchart TD | Close | 1) "Faster onboarding" goal supported by an eKYC requirement<br>2) "Lower fraud losses" supported by two requirements<br>3) Conflict between speed and strict verification goals |
| Value Stream Map | flowchart LR with wait-time labels | Close | 1) Loan flow: intake, credit check, approval, signing<br>2) Card dispute handling with handoffs<br>3) Invoice-to-payment with manual steps highlighted |
| Business–Application Alignment | block-beta grid (capabilities as rows, applications as columns) | Close | 1) Payments capabilities mapped to three applications<br>2) Customer servicing with overlapping CRM tools<br>3) Reporting capability with no owning application |
| Application Portfolio Map | quadrantChart (business value vs technical health) | Close | 1) Five applications placed by value and health<br>2) Legacy mainframe: high value, low health<br>3) Duplicate survey tool: low value, high health, so retire |

## System Context, Boundaries & Decomposition

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| System Landscape (C4) | C4Context with several System nodes | Native | 1) Bank systems: CRM, core, cards, data platform<br>2) Two systems both owning customer addresses<br>3) Shared identity provider used by four systems |
| System Context (C4 L1) | C4Context | Native | 1) Mobile banking app with customer, core banking, payment provider<br>2) Fraud tool with analyst and card network<br>3) Batch file exchange with regulator |
| Container (C4 L2) | C4Container | Native | 1) Web app, API, database, queue for an order service<br>2) Mobile backend-for-frontend and core service<br>3) Scheduler and worker for nightly reconciliation |
| Component (C4 L3) | C4Component | Native | 1) Payment service: validator, router, ledger adapter<br>2) Auth service: token issuer, user store adapter<br>3) Notification service: template engine, channel senders |
| Code (C4 L4) | classDiagram | Close | 1) Account class with Savings and Current subclasses<br>2) Repository interface with JDBC implementation<br>3) Strategy classes for fee calculation |
| Package Diagram (UML) | classDiagram with namespace, or flowchart with subgraphs | Close | 1) Payments, accounts, and reporting modules with dependencies<br>2) Dependency cycle between two packages<br>3) Shared kernel package used by all modules |
| Component Diagram (UML) | classDiagram with `<<interface>>`, or C4Component | Close | 1) PaymentService interface with two implementations<br>2) Provided and required interfaces of a pricing component<br>3) Replaceable fraud scoring component |
| Composite Structure Diagram | block-beta with nested blocks as parts | Approximate | 1) Order processing system composed of parts<br>2) ATM with card reader, cash unit, screen<br>3) Trading engine with matching and risk parts |
| Layered Architecture | block-beta with stacked rows | Close | 1) Presentation, API, domain, persistence layers<br>2) Channel layer over shared services<br>3) Highlighted layer violation with direct database access |
| Hexagonal / Ports-and-Adapters | flowchart with core subgraph and adapter nodes | Approximate | 1) Loan domain core with REST and Kafka adapters<br>2) Payment core with bank gateway adapter<br>3) Test double adapter replacing the database |

## Software Structure, Object Models & Design

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Domain Driven Design (method) | mindmap for bounded contexts and aggregates | Approximate | 1) Banking domain split into contexts<br>2) Aggregates inside the account context<br>3) Ubiquitous language glossary tree |
| Class Diagram (UML) | classDiagram | Native | 1) Account, Transaction, Customer classes<br>2) Strategy pattern for interest calculation<br>3) Enum for order status |
| Object Diagram (UML) | flowchart with instance nodes | Approximate | 1) Customer snapshot with two accounts<br>2) Loan with linked installments<br>3) Order with lines and payment objects |
| Profile Diagram (UML) | classDiagram with `<<stereotype>>` annotations | Approximate | 1) Stereotypes for PII and audited fields<br>2) Profile marking aggregate roots<br>3) Data classification levels as tags |
| Domain Model Diagram | classDiagram | Native | 1) Loan application with Applicant and Offer<br>2) Insurance policy with coverages<br>3) Payment with status and amounts |
| Bounded Context Map | flowchart with subgraphs and labeled relations | Approximate | 1) Sales and Billing contexts with customer-supplier link<br>2) Anti-corruption layer to legacy core<br>3) Shared kernel for money and currency types |
| Aggregate Diagram | classDiagram with composition | Close | 1) Order aggregate with order lines<br>2) Account aggregate with transactions as consistency boundary<br>3) Customer aggregate with addresses |

## Runtime Behavior, Interactions & State

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Sequence Diagram (UML) | sequenceDiagram | Native | 1) Card payment authorization<br>2) Login with MFA<br>3) Account transfer with timeout |
| Communication Diagram (UML) | flowchart with numbered edges | Approximate | 1) Loan approval objects with numbered messages<br>2) Order collaboration across three services<br>3) Batch job with reader and writer |
| Activity Diagram (UML) | flowchart TD with parallel branches | Close | 1) Onboarding with parallel KYC and credit checks<br>2) Claims handling with decisions<br>3) Month-end closing steps |
| State Machine Diagram (UML) | stateDiagram-v2 | Native | 1) Payment states: initiated, authorized, settled, failed<br>2) Loan application lifecycle<br>3) Card states: active, blocked, expired |

## Distributed Systems

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Saga / Distributed Transaction | sequenceDiagram with alt for compensation | Close | 1) Order saga: reserve stock, charge, ship, with compensation<br>2) Transfer across two ledgers with rollback<br>3) Travel booking: flight, hotel, car |
| Request Lifecycle | sequenceDiagram, or flowchart LR | Close | 1) API request through gateway, auth, service, database<br>2) Validation failure short-circuiting at gateway<br>3) Cache hit path vs cache miss path |

## Business Processes, Workflows & Decisions

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Use Case Diagram (UML) | flowchart LR with actors and a system subgraph | Approximate | 1) Customer use cases in mobile banking<br>2) Advisor use cases in CRM<br>3) Admin use cases with include relation |
| Process Diagram (BPMN) | flowchart with BPMN-like shapes (events, gateways, subprocesses) | Approximate | 1) Loan approval with decision gateway<br>2) Complaint handling with escalation path<br>3) Parallel document checks |
| Customer Journey Map | journey | Native | 1) Opening an account across branch and app<br>2) Card replacement with satisfaction scores<br>3) Mortgage application with handoffs |

## Data Architecture & Information Modeling

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Entity–Relationship Diagram (ERD) | erDiagram | Native | 1) Customer, Account, Transaction<br>2) Product, Order, OrderLine<br>3) Policy, Coverage, Claim |
| Conceptual Data Model | erDiagram with entity and relationship names only | Native | 1) Customer, Contract, Product concepts<br>2) Party roles in insurance<br>3) Payment and settlement concepts |
| Logical Data Model | erDiagram with keys and cardinalities | Native | 1) Account with PK and FK, normalized transactions<br>2) Customer-product many-to-many via bridge table<br>3) Address as a separate entity |
| Physical Data Model | erDiagram with column types and keys | Native | 1) Accounts table with DECIMAL(18,2) balance<br>2) Partitioned transactions table<br>3) Audit columns on every table |
| Data Flow Diagram (DFD) | flowchart with circles for processes and cylinders for stores | Close | 1) Payment processing with a ledger store<br>2) Complaint flow with external customer entity<br>3) Monthly reporting data flow |

## Data Warehouse

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Data Lineage Diagram | flowchart LR | Close | 1) Core banking to staging to data mart to risk report<br>2) Column transformation chain<br>3) Impact of renaming a source field |
| Data Ownership / System-of-Record Map | flowchart with subgraphs per domain | Close | 1) Customer master owned by CRM<br>2) Product catalog owned by pricing team<br>3) Conflicting customer address sources |
| Data Lifecycle Diagram | stateDiagram-v2, or timeline | Close | 1) Transaction data: active, archived, deleted<br>2) Log retention milestones<br>3) GDPR deletion after account closure |
| Data Pipeline / ETL DAG | flowchart LR, or gantt for schedules | Close | 1) Nightly ingest, transform, validate, load<br>2) Parallel extracts merged into a fact table<br>3) Retry path on failed validation |

## Integration, APIs & Distributed Systems

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Integration Architecture Diagram | architecture-beta, or flowchart LR | Close | 1) Core banking integrated via ESB and API gateway<br>2) Batch file exchange with regulator<br>3) Event bus between CRM and marketing |
| API Contract / Interface Map | classDiagram with `<<interface>>` and endpoints as methods | Close | 1) Payments API v1 and v2 consumers<br>2) Customer API used by three apps<br>3) Partner API with versioned endpoints |
| Event-Driven Architecture Diagram | flowchart LR with topics as nodes | Close | 1) OrderPlaced consumed by billing and shipping<br>2) Fraud alerts to case management<br>3) Account updated event to reporting |
| Message Routing Diagram | flowchart LR with router and dead-letter path | Close | 1) Content-based router splitting payment types<br>2) Enricher adding customer data<br>3) Dead-letter queue for failed messages |
| Event Storming Board (DDD) | flowchart with classDef sticky-note colors | Approximate | 1) Loan application events and commands<br>2) Policy blocking card after fraud event<br>3) Hotspot marking unclear ownership |
| CQRS Read/Write Architecture | flowchart with command and query subgraphs | Close | 1) Account commands writing ledger, read model for app<br>2) Projection updating search index<br>3) Eventual consistency lag on read path |
| Distributed Consistency / Replication | sequenceDiagram with quorum writes | Close | 1) Leader write replicated to two followers<br>2) Quorum read during network partition<br>3) Concurrent update conflict resolution |

## Infrastructure, Deployment & Network Architecture

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Deployment Diagram (UML / C4) | C4Deployment | Native | 1) Web and API nodes on a Kubernetes cluster<br>2) Database primary and standby on VM hosts<br>3) On-premise core with cloud services |
| Infrastructure Topology | architecture-beta, or flowchart with subgraphs | Close | 1) Load balancer, two app servers, database<br>2) Storage and backup servers<br>3) Monitoring stack beside workloads |
| Cloud Architecture Diagram | architecture-beta with cloud, database, and server icons | Close | 1) Web app with CDN, API, managed database in one region<br>2) Serverless event pipeline<br>3) Subscription boundaries as groups |
| Network Topology Diagram | flowchart with zone subgraphs and firewall nodes | Close | 1) DMZ, application zone, data zone with firewalls<br>2) Branch VPN to head office<br>3) Internet ingress through WAF |
| High-Availability / Multi-Region | flowchart with region and zone subgraphs | Close | 1) Active-passive region failover<br>2) Three-zone database cluster<br>3) DNS failover between regions |
| Cluster / Orchestration | block-beta grid, or flowchart with subgraphs | Approximate | 1) Kubernetes namespaces with deployments<br>2) Node pools with autoscaling<br>3) Ingress routing to services |
| Environment / Release Topology | flowchart LR, with gitGraph for release branches | Close | 1) Dev, test, staging, prod promotion path<br>2) Configuration differences per environment<br>3) Hotfix path to production |

## Security, Privacy & Trust

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Trust Boundary Diagram | flowchart with subgraphs as trust zones | Close | 1) Internet, DMZ, internal network<br>2) Partner network crossing a boundary<br>3) Browser to API boundary with authentication |
| Threat Modeling DFD | flowchart with classDef per trust zone | Close | 1) Login flow with spoofing risk marked<br>2) Data store with tampering risk<br>3) Admin API with privilege escalation risk |
| Attack Tree | mindmap, or flowchart TD with AND/OR labels | Close | 1) Attacker steals customer credentials<br>2) Attacker tampers with payment amount<br>3) Insider exports customer data |
| Identity & Authorization Flow | sequenceDiagram | Native | 1) OAuth2 authorization code flow<br>2) Service-to-service token exchange<br>3) MFA step-up for large transfers |
| Security Zone / Segmentation | block-beta with zone blocks | Close | 1) Public, internal, restricted zones for databases<br>2) PCI zone isolated from marketing<br>3) Management network for admin access |
| Sensitive Data Flow / Privacy Map | flowchart LR with classDef highlighting PII | Close | 1) Customer PII flowing to CRM and analytics<br>2) Card number tokenized before logging<br>3) Data sent to external credit bureau |

## Reliability, Performance & Quality Attributes

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Quality Attribute Scenario | requirementDiagram | Close | 1) 95% of payments under 300 ms at peak<br>2) 99.9% availability during business hours<br>3) Restore service within 1 hour after failure |
| Fault Tree Analysis (FTA) | flowchart TD with AND/OR gate nodes | Approximate | 1) Outage from database and failover both failing<br>2) Data loss from two simultaneous disk failures<br>3) Payment failure from timeout or config error |
| Reliability Block Diagram (RBD) | flowchart LR with parallel branches | Approximate | 1) Two redundant app servers in series with database<br>2) Redundant load balancers<br>3) Dual network paths |
| Failure Propagation Diagram | flowchart LR with timeout and fallback nodes | Close | 1) Payment slowdown exhausting thread pool<br>2) Fraud service outage triggering fallback<br>3) Cache failure overloading database |
| Capacity / Queuing Model | xychart-beta (load vs latency), plus flowchart for queues | Close | 1) Response time curve vs requests per second<br>2) Queue served by three workers<br>3) Throughput before and after scaling |
| Service Dependency / Health Model | flowchart with classDef health colors | Close | 1) Checkout depending on payments, catalog, auth<br>2) Degraded search service on critical path<br>3) Regional outage dependency map |

## Architecture Evolution, Migration & Planning

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Baseline vs. Target Architecture | flowchart with two subgraphs | Close | 1) Monolith vs microservices for orders<br>2) On-premise vs cloud hosting<br>3) Batch vs event-driven reporting |
| Transition Architecture (ArchiMate) | flowchart with baseline, transition, and target subgraphs | Close | 1) Old and new payments coexisting<br>2) Dual-running CRM integration<br>3) Temporary bridge component |
| Migration Roadmap / Plateau | gantt, or timeline | Close | 1) Q1 foundation, Q2 pilot, Q3 cutover plateaus<br>2) Mainframe retirement phases<br>3) Milestones per business domain |
| Strangler Migration | flowchart with facade routing to old and new | Close | 1) Facade routing claims endpoints to new service<br>2) Accounts migrated gradually by product<br>3) Legacy endpoint retired at 100% traffic |
| Migration Dependency Graph | flowchart LR, with gantt for critical path | Close | 1) Data migration blocking API cutover<br>2) Compliance approval blocking go-live<br>3) Team training gating rollout |
| Change Impact Diagram | mindmap, or flowchart LR | Close | 1) Customer ID format change impacting five systems<br>2) New field in account API affecting reports<br>3) Regulation change touching three processes |

## Architecture Evaluation & Decision Support

| Diagram type | Mermaid alternative | Fit | Simple example ideas |
|---|---|---|---|
| Trade-off Map | radar-beta, or quadrantChart | Close | 1) Cloud vs on-premise scored on cost, speed, control<br>2) Three options compared on quality attributes<br>3) Build vs buy comparison |
| Decision Tree | flowchart TD | Close | 1) Database choice by consistency and scale needs<br>2) Sync vs async integration choice<br>3) Hosting option by data residency rule |
| Architecture Risk Map | quadrantChart (impact vs likelihood) | Close | 1) Legacy core dependency: high impact, high likelihood<br>2) Vendor lock-in risk<br>3) Skills gap risk |
| Sensitivity / Trade-off Point Map (ATAM) | mindmap as utility tree | Close | 1) Latency and availability under utility tree<br>2) Cache size as sensitivity point for latency<br>3) Encryption as trade-off point for throughput |
| Dependency Structure Matrix (DSM) | block-beta grid with colored cells | Approximate | 1) Dependency matrix of five services<br>2) Cycle between billing and orders<br>3) Tightly coupled cluster of components |
| Architecture Fitness Function Map | mindmap, or flowchart LR | Close | 1) UI layer must not access database, checked in pipeline<br>2) Response time test in CI<br>3) Dependency rule enforced by lint |

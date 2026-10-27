# Modeling Process
Tools and notations


# Enterprise Architecture & Business Strategy


- Capability Map (ArchiMate)
    - Hierarchical map of what an organization must be able to do, independently of its organizational structure.
    - Answers: 
        - What capabilities does the business need? Which are missing, duplicated, weak, or strategically important?
    - Stakeholders:    
        - Business Executive: Which capabilities are strategically critical but underdeveloped?
        - Enterprise Architect: Where are overlapping or missing capabilities?
        - Portfolio Manager: Where should modernization investments go?

https://ariscommunity.com/users/q2y5np9c6o38/2019-10-07-capability-based-planning-archimate-and-aris


- Business Motivation Diagram (ArchiMate)
    - Connects stakeholders, drivers, assessments, goals, outcomes, principles, and requirements.
    - Answers: 
        - Why are we changing the architecture? What objectives, pressures, and constraints justify the change?
    
    - Stakeholders:    
        - Business Sponsor: Why do we need this transformation?
        - Solution Architect: Which business drivers constrain our design options?
        - Compliance Officer: Which regulatory obligations must the solution satisfy?

- Stakeholder Viewpoint (ArchiMate)
    - Maps stakeholders to their concerns, drivers, assessments, and desired outcomes.
    - Answers: Who cares about the change? What competing interests must be reconciled?

- Goal Realization Diagram (ArchiMate)
    - Shows how goals are refined and supported by outcomes, requirements, and other goals.
    - Answers: How do architectural requirements contribute to business objectives?


- Value Stream Map (ArchiMate / business architecture)
    - Models stages through which an organization creates value for customers or stakeholders.
    - Answers: Where is value created? Where are delays, handoffs, and improvement opportunities?

    - Stakeholders:
        - Operations Manager: Where are delays and handoffs reducing efficiency?
        - Product Manager: Where does the customer receive measurable value?
        - Enterprise Architect: Which stages could be automated or redesigned?

- Business–Application Alignment (Capability-Service Map) Diagram
    - Maps business capabilities, processes, and services to supporting applications.
    - Answers: Which applications support which business functions? Where are capability gaps or redundant systems?

    - Stakeholders:
        - Business Owner: Which applications support my business processes?
        - Enterprise Architect: Where do multiple applications provide overlapping functionality?
        - Product Manager: Which business capabilities would be affected by retiring an application?

- Application Portfolio Map
    - Visualizes applications by business importance, technical health, lifecycle, cost, or strategic fit.
    - Answers: Which applications should we invest in, modernize, consolidate, or retire?

    - Stakeholders:
        - CIO: Which applications should we modernize, consolidate, or retire?
        - Finance Director: Where are we spending money on low-value applications?
        - Enterprise Architect: Which legacy applications create the greatest architectural constraints?


# System Context, Boundaries & Decomposition

- System Landscape Diagram (C4)
    - Overview of multiple software systems and their relationships across an organization.
    - Answers: What systems exist? Which depend on each other? Where do responsibilities overlap?

- System Context Diagram (C4 Level 1)
    - Shows one system in relation to users, external systems, and integrations.
    - Answers: What is inside and outside our scope? Who interacts with the system? What external dependencies exist?

- Container Diagram (C4 Level 2)
    - Decomposes a system into applications, services, databases, and other runnable or storage units.
    - Answers: What are the major technical building blocks? What responsibilities and technologies do they have? How do they communicate?

- Component Diagram (C4 Level 3)
    - Shows the major logical components inside a particular application or service.
    - Answers: How is this service internally organized? Where are its interfaces and dependencies?

- Code Diagram (C4 Level 4)
    - Describes implementation structures using classes, interfaces, functions, or other code-level constructs.
    - Answers: How is a component implemented? Which code elements collaborate?


## Boundaries & Decomposition

- Package Diagram (UML)
    - Shows logical packages, namespaces, modules, and dependencies between them.
    - Answers: How should the codebase be partitioned? Which modules depend on which others? Where are dependency cycles?

    - Ownership (Teams), Versioning, Dependencies  - Whats deployed together

- Component Diagram (UML)
    - Models components with provided and required interfaces and dependency relationships.
    - Answers: What contracts connect components? Can one implementation be replaced without changing its consumers?

    - Ownership (Teams), Versioning, Dependencies - What talks to what

- Composite Structure Diagram (UML)
- Layered Architecture Diagram
- Hexagonal / Ports-and-Adapters Diagram


# Software Structure, Object Models & Design
- Domain Driven Design

- Class Diagram (UML)
    - Shows classes, attributes, operations, associations, composition, and inheritance.
    - Answers: What are the types and their relationships? Which abstractions own which responsibilities?

- Object Diagram (UML)
    - Shows a snapshot of concrete object instances and links at a particular moment.
    - Answers: What does a valid runtime object structure look like? Can the model represent this specific scenario?

- Profile Diagram (UML)
    - Defines domain-specific extensions to UML using stereotypes, tagged values, and constraints.
    - Answers: How can standard UML concepts be customized consistently for a particular domain?

# Pipe, Pipe, pipe ... - Shared, Ubiqitous Language  - Busines <> Code 

- Domain Model Diagram (DDD / UML-like)
    - Represents business concepts, relationships, invariants, and shared vocabulary.
    - Answers: What concepts exist in the problem domain? Which distinctions matter to business rules?

- Bounded Context Map (DDD)
    - Shows bounded contexts and relationships such as Customer–Supplier, Shared Kernel, or Anti-Corruption Layer.
    - Answers: Where should model boundaries exist? Which teams or systems must translate concepts between contexts?

- Aggregate Diagram (DDD)
    - Shows aggregate roots, internal entities, value objects, and consistency boundaries.
    - Answers: What must change atomically? Where are transactional invariants enforced?


# Runtime Behavior, Interactions & State

- Sequence Diagram (UML)
    - Shows messages exchanged between participants in chronological order.
    - Answers: What happens during this scenario? Who calls whom? Where do retries, timeouts, and failures occur?

- Communication Diagram (UML)
    - Emphasizes collaborating objects and their message relationships, with ordering labels.
    - Answers: Which objects communicate? How are responsibilities distributed across participants?


- Activity Diagram (UML)
    - Shows control flow, decisions, concurrent activities, and object flows.
    - Answers: What steps are performed? What branches or parallel work can occur?

- State Machine Diagram (UML)
    - Models states, events, guards, actions, and transitions for an entity or system.
    - Answers: What states are valid? Which transitions are permitted? What happens on an unexpected event?

# Distributed systems

- Saga / Distributed Transaction Diagram
    - Shows distributed transaction steps, local commits, compensations, and failure paths.
    - Answers: How is a business operation completed without one global transaction? What happens after partial failure?

- Request Lifecycle Diagram
    - Traces a request through authentication, validation, orchestration, processing, storage, and response generation.
    - Answers: Where is time spent? Which components can reject or transform a request? Where does failure propagate?

# Business Processes, Workflows & Decisions 

- Use Case Diagram (UML)
    - Shows actors, system capabilities, and relationships between use cases.
    - Answers: What functionality does the system expose? Who initiates or participates in each interaction?

- Process Diagram (BPMN)
    - Models business activities, events, gateways, conditions, and execution paths.
    - Answers: How does a business process work? What happens next? Where are decisions, exceptions, and parallel activities?

- Customer Journey Map
    - Shows customer stages, interactions, goals, frustrations, and experiences.
    - Answers: What does the customer experience across channels? Where do organizational or system boundaries harm that experience?


# Data Architecture & Information Modeling

- Entity–Relationship Diagram (ERD)
    - Represents entities, attributes, identifiers, and relationships.
    - Answers: What data exists? How are entities related? What integrity constraints are necessary?


- Conceptual Data Model
    - High-level representation of business information, independent of database technology.
    - Answers: What information concepts are important to the business? What do different stakeholders mean by the same terms?

- Logical Data Model
    - Defines data structures, keys, relationships, cardinalities, and constraints without tying them to a specific DBMS.
    - Answers: How should information be structured consistently? Which entities and relationships need normalization?

- Physical Data Model
    - Represents concrete tables, columns, types, keys, indexes, and storage-specific structures.
    - Answers: How will data actually be persisted? What schema and database constraints will be implemented?

- Data Flow Diagram (DFD)
    - Shows processes, external entities, data stores, and movement of information.
    - Answers: Where does information originate, move, and get transformed? What information crosses system boundaries?

# Data warehouse

- Data Lineage Diagram
    - Traces information through source systems, transformations, intermediate datasets, and destinations.
    - Answers: Where did this data come from? What downstream reports, models, or services are affected if a source changes?

- Data Ownership / System-of-Record Map
    - Maps information domains to their authoritative owners and consuming systems.
    - Answers: Which system owns each piece of data? Who may update it? Where are conflicting sources of truth?

- Data Lifecycle Diagram
    - Models data from creation and processing through retention, archival, and deletion.
    - Answers: How long is data retained? When must it be deleted? Which regulatory or operational obligations apply?

- Data Pipeline / ETL DAG
    - Shows extraction, transformation, validation, loading, and dependency relationships.
    - Answers: In what order must datasets be processed? What happens if a transformation fails? Which stages can run in parallel?


# Integration, APIs & Distributed Systems

- Integration Architecture Diagram
    - Maps systems, APIs, brokers, integration middleware, protocols, and connections.
    - Answers: How are systems integrated? Which integrations are synchronous, asynchronous, or batch-based?

- API Contract / Interface Map
    - Shows provided and consumed interfaces, endpoints, versions, and dependencies.
    - Answers: Which contracts connect systems? Who depends on which API? What could break after a contract change?

- Event-Driven Architecture Diagram
    - Maps event producers, brokers, topics, subscriptions, and consumers.
    - Answers: How are events distributed? Where is coupling introduced? What are the delivery and ordering dependencies?

- Message Routing Diagram
    - Shows routing, filtering, transformation, enrichment, aggregation, and delivery paths.
    - Answers: How does a message reach the correct destination? Where are transformations, retries, and dead-letter handling applied?

- Event Storming Board (DDD)
    - Uses domain events, commands, actors, policies, and aggregates to explore business behavior.
    - Answers: What actually happens in the domain? What triggers actions? Where might consistency and ownership boundaries belong?

- CQRS Read/Write Architecture Diagram
    - Separates commands, authoritative write models, projections, and query/read models.
    - Answers: Where is authoritative state changed? How are read models updated? Where can eventual consistency arise?

- Distributed Consistency / Replication Diagram
    - Shows leaders, replicas, synchronization, quorum, and consistency relationships.
    - Answers: How does information propagate between nodes? What happens during network partitions or concurrent updates?


# Infrastructure, Deployment & Network Architecture

- Deployment Diagram (UML / C4 variants)
    - Maps software artifacts, services, and containers onto execution environments and infrastructure nodes.
    - Answers: Where does software run? Which nodes host which elements? How are runtime components connected?

- Infrastructure Topology Diagram
    - Shows servers, load balancers, databases, storage, networking, and supporting infrastructure.
    - Answers: What infrastructure is required? What depends on what? Where could bottlenecks or single points of failure exist?

- Cloud Architecture Diagram
    - Represents managed services, regions, accounts, subscriptions, storage, compute, and connectivity.
    - Answers: Which cloud services implement the solution? Where are costs, operational responsibilities, and provider dependencies introduced?

- Network Topology Diagram
    - Shows networks, subnets, routers, firewalls, gateways, and connections.
    - Answers: Which network paths exist? What can communicate with what? Where are routing, bandwidth, or isolation constraints?

- High-Availability / Multi-Region Diagram
    - Shows redundant components, availability zones, regions, failover paths, and replication relationships.
    - Answers: What continues working after a node, zone, or region fails? Which shared dependencies remain?

- Cluster / Orchestration Diagram
    - Shows Kubernetes clusters or equivalent orchestration structures, workloads, services, ingress, and scaling groups.
    - Answers: How are workloads scheduled and exposed? How are failures handled and capacity scaled?

- Environment / Release Topology
    - Maps development, testing, staging, production, and their configuration or data dependencies.
    - Answers: Where is software validated before release? Which environments differ? How is production isolated?


# Security, Privacy & Trust

- Trust Boundary Diagram
    - Shows components, data flows, and boundaries between different levels of trust.
    - Answers: Where does untrusted input enter? Which interactions require authentication, validation, or other controls?

- Threat Modeling DFD
    - Represents processes, data stores, flows, and trust boundaries for systematic threat analysis.
    - Answers: What can be attacked? Where could spoofing, tampering, information disclosure, or privilege escalation occur?

- Attack Tree
    - Decomposes an attacker objective into possible strategies and prerequisite actions.
    - Answers: How could an attacker achieve a specific outcome? Which preventive or detective controls interrupt the attack?

- Identity & Authorization Flow Diagram
    - Models identity providers, applications, tokens, authentication, delegation, and authorization checks.
    - Answers: Who authenticates whom? Where are permissions enforced? How do identities and credentials flow through the system?

- Security Zone / Segmentation Diagram
    - Organizes systems into zones based on sensitivity, trust, and allowed communication.
    - Answers: Which assets must be isolated? Where should firewalls, gateways, and access restrictions be enforced?

- Sensitive Data Flow / Privacy Map
    - Traces personal or sensitive information through systems, processors, storage, and external recipients.
    - Answers: Where is sensitive information processed? Who can access it? What privacy obligations and exposure risks exist?


# Reliability, Performance & Quality Attributes

- Quality Attribute Scenario Diagram
    - Connects a stimulus source, stimulus, environment, affected artifact, response, and measurable response.
    - Answers: What should happen under a specific operational condition? How will we know the quality requirement is met?

- Fault Tree Analysis (FTA)
    - Uses logical gates to decompose an undesirable failure into contributing events and conditions.
    - Answers: What combinations of failures could cause an outage or other unacceptable outcome? Which failures deserve mitigation?

- Reliability Block Diagram (RBD)
    - Models series, parallel, and redundant dependencies affecting system reliability.
    - Answers: How do component reliabilities combine? How much availability can redundancy improve?

- Failure Propagation Diagram
    - Shows how failures, congestion, timeouts, or resource exhaustion can spread through dependencies.
    - Answers: What is the blast radius of a failure? Where should isolation, circuit breakers, or fallback behavior be introduced?

- Capacity / Queuing Model
    - Represents request arrival rates, service capacity, queues, workers, and resource limits.
    - Answers: Where will bottlenecks form? How will latency and throughput change as load increases?

- Service Dependency / Health Model
    - Maps services and dependencies with health signals and degradation states.
    - Answers: What determines whether the system is healthy? Which dependency failures affect critical user journeys or SLOs?


# Architecture Evolution, Migration & Planning

- Baseline vs. Target Architecture Diagram
    - Compares the current architecture with the desired future structure.
    - Answers: What must change? Which current limitations are removed? Which new dependencies are introduced?

- Transition Architecture Diagram (ArchiMate)
    - Represents intermediate architectural states between baseline and target.
    - Answers: What viable intermediate states can the organization operate in? What must coexist during migration?

- Migration Roadmap / Plateau Diagram (ArchiMate)
    - Shows architectural plateaus, implementation work, gaps, and transitions over time.
    - Answers: In what order should changes occur? What dependencies constrain the migration sequence?

- Strangler Migration Diagram
    - Shows legacy and replacement systems coexisting while responsibilities are incrementally redirected.
    - Answers: Which capabilities can be migrated independently? How is traffic switched? When can the legacy implementation be retired?

- Migration Dependency Graph
    - Shows technical, business, data, and organizational prerequisites between migration tasks.
    - Answers: What must happen first? Which tasks block other work? Where is the critical path?

- Change Impact Diagram
    - Maps a proposed change to affected services, interfaces, data stores, business processes, and stakeholders.
    - Answers: What else might break or require modification? Who must coordinate or approve the change?


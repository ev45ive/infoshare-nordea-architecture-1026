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


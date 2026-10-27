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


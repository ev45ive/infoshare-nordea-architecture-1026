
# Enteprise Architecture Design

- Enterprise-wide blueprint aligning
    - business strategy
    - processes, organization
    - data
    - Portfolio of systems (landscape)
    - capabilities (e.g. payments, onboarding, risk, it)

👉 Often formalized using frameworks like TOGAF

👉 Think: Capability/Process to Systems mapping 
Long-term transformation (e.g. “move to cloud”, “become API-first”)

### Artifacts
- Capability maps
- Value streams
- Target architecture (future state)
- Roadmaps (multi-year)
- Principles (e.g. “cloud-first”, “event-driven”)

# Example
👉 Abstract, strategic, slow-changing

“In 3 years, all customer data will be centralized and exposed via APIs across all channels.”


---

# Solution Architecture Design
- Describing Problem / Goals
- A decision-making process about structure, technologies, and tradeoffs

- A bridge between:
    - business (goals, OKRs, KPIs, constraints)
    - engineering (implementation, scalability, reliability)

- A set of models + documents that guide delivery teams

### Process
- Understand problem
- Define requirements (NFR) 
- Explore possibilities / constraints  
- Decide tradeoffs and intent
- Design system - data, flows, APIs
- Validate against stakeholders: business <> engineers
- Support implementation - code review, adjust design on reality


👉 Think: “Given this messy reality, what system shape gives the best outcomes?”
X Do not try to model the universe - Think: "What NOT to include?"


### Tasks
- Define system structure
- Select technologies with justification
- Identify risks and tradeoffs
- Ensure non-functional requirements:
- scalability
- reliability
- security
- performance
- Enable team alignment


## Artifacts 
- Architecture diagrams
    - Context diagram (system in environment)
    - Container diagram (services/apps)
    - Component diagram (internal structure)
    - Sequence diagrams (flows)
  👉 Often using C4 model


- Architecture Decision Records (ADR)
    - What are we doing
    - What are the problems
    - What are possible solutions
    - Contraints / Tradeoffs / Risk
    - Decision + Why
    - Why Alternatives were rejected
Consumers (Stakeholders): Devs, Manager, Integration/Teams, DevOps, etc...

👉 Critical for why, not just what


- System design document
- Domain model
- API contracts
- Data architecture
- Operational design (SLO,SLA,Metrics,Incident management)

--- 
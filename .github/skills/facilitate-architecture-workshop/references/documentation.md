# Documentation

Read when producing or revising working records, ADRs, diagrams, domain/data/API models,
delivery estimates, or checkpoint artifacts. Use only the subsection needed now.

## Choose the smallest useful artifact

| Question | Suitable artifact |
| --- | --- |
| What is our scope, environment, or deployment? | Context/container/deployment view |
| What happens through time, failure, retry, or recovery? | Sequence/state/data-flow view |
| Who owns a concept, decision, invariant, or integration? | Domain/context/ownership map |
| What does a UI journey require of data and behavior? | Annotated mockup, API examples, lifecycle/model sketch |
| Why choose this option and what does it cost? | Short ADR |
| What can this team deliver, and when? | Capacity estimate and Gantt/dependency view |
| Which business commitment should change? | Stakeholder message and recorded disposition |

Do not require every diagram or all notation types at every stage. Ask which audience
needs which answer. Use minimal notation, explicit boundaries, labeled relationships,
ownership, state, and assumptions. Include a legend where necessary. Keep implementations
and runnable UI prototypes optional, subject to authorized task scope and cost accounting.

Distinguish UI behavior, API contract, domain concept, persistence schema, deployment
unit, and team ownership. Check that their mappings are explicit rather than assumed.
Do not require them to share names or one-to-one boundaries.

## Minimal records

Use designated session paths. If organizing a new local session, propose a few records
rather than an elaborate knowledge system. Combine evidence, decisions, resources, and
risks initially; split when size justifies it. Keep:

- A control/current-state view pointing at active evidence and the last checkpoint.
- An append-only accepted decision/resource history with clearly labeled working drafts.
- Versioned artifacts and immutable accepted phase snapshots.

Follow current runtime file-saving rules; do not assume a sandbox link persists a file.
Do not move Library-backed or externally owned items without authorization. Keep paths
and identifiers stable and exact. Save only workshop deliverables, not hidden authoring
material or unrelated user data.

## Short decision entry / ADR

- ID, phase, status, scenario time, and author/decision owner.
- Decision question; current context, stakes, evidence pointers, and assumptions.
- Credible alternatives, including delay/negotiation where relevant.
- Chosen action and why under these conditions; what would favor an alternative.
- Incurred/committed/estimated costs, second-order effects, operational responsibilities.
- Promises affected, accepted risks/debt, options closed/preserved, revisit trigger.
- Linked artifact versions and superseded decision IDs where applicable.

Preserve participant reasoning. Offer a draft if helpful; do not retrospectively invent
a rationale they never supplied. An explicit participant choice can authorize its record;
ask only when acceptance, material costs, or consequences remain ambiguous.

Keep earlier decisions unchanged when superseded. Append the new decision and update
the current-state index. Freeze accepted artifact versions; create a new version for a
change. Do not silently replace a diagram to make earlier choices look better informed.

## Evidence and uncertainty

For significant claims, link source ID and relevant location. Classify observations,
stakeholder interpretations, contractual commitments, technical mechanisms, estimates,
assumptions, and unknowns. Preserve disagreements rather than merging them into a false
consensus. Record pending investigations with their decision impact and next action.

## Delivery plan and resource record

Keep scope, role/skill, person-days or ranges, dependencies, staffing assumptions,
contingency, operational load, and critical sequence visible. Distinguish person-days
from elapsed days; parallelism depends on available skills and dependencies. Treat
learning, verification, integration, and rollout as work. Link costs to decision/event
IDs. Use the Constraints and economics reference from the core skill when estimating.

## Final artifact check

Can another developer, analyst, or stakeholder understand what is proposed, why, under
which conditions, with what cost and consequence? Does the diagram answer its stated
question? Are draft/accepted statuses and source links clear? Keep formatting subordinate
to that purpose. No exhaustive paperwork or implementation-mirroring tests are required.

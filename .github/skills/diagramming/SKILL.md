---
name: diagramming
description: Fast system architecture diagramming with Mermaid in plain .md files for VS Code. Use when asked to draw, fix, or layout architecture diagrams, architecture-beta with logo icons, or to map a UML diagram type to Mermaid. Covers decision rules, architecture-beta layout tricks, verified VS Code icon packs, and a UML-to-Mermaid cheatsheet.
---

# Diagramming (Mermaid in VS Code .md)

## Goal

Produce a working diagram in a plain `.md` file that renders in the VS Code Markdown preview with no installs and no config. Verify by name, not by memory.

## Workflow

1. **Pick the diagram type** with the decision rules below. Read the matching file in `diagrams/uml/` or `diagrams/architecture/` for repo conventions.
2. **Check icon names** against the bundled packs (see "Icons") before using them. Do not guess.
3. **Write the diagram** in a fenced ` ```mermaid ` block inside a `.md` file. Use the repo file layout: a title, a one-line "Mermaid type" note, the diagram, then a Legend and Notes if icons are used.
4. **Lay out** with `align` (architecture-beta) or by reducing edges. Keep edges short and mostly between neighbours.
5. **Verify**: the user refreshes the VS Code Markdown preview (`Ctrl+Shift+V`). Only claim a render after the user confirms, or after a headless render check.
6. **Clean up** any temp files. Do not create planning or notes files unless asked.

## Decision rules

| Need | Use |
|---|---|
| Cloud or system architecture with vendor icons | `architecture-beta` (beta, limited) |
| Components, deployment nodes, pods, flows, many node shapes | `flowchart` with `subgraph` |
| Class or domain model | `classDiagram` |
| Request/response, auth flow, retries | `sequenceDiagram` |
| Object lifecycle, states, guards | `stateDiagram-v2` |
| Timing with a shared time axis | Not supported. Use PlantUML (`@startuml` with `concise` or `robust`). `gantt` is not a substitute. |
| Pixel-exact positions or free layout | Not Mermaid. Use draw.io or similar. |

Rules of thumb:
- Architecture overview with icons: `architecture-beta`.
- Anything with more than about 25 nodes or many crossing edges: split into two diagrams (runtime vs. data/ops), not one.
- Prefer `flowchart` when the user needs shapes, conditionals, or subgraph nesting beyond groups.

## architecture-beta

### Syntax essentials
- `group id(icon)[Label]`
- `service id(icon)[Label] in group`
- `junction id in group`
- Edges: `svcA:SIDE --> SIDE:svcB`. `SIDE` is `L`, `R`, `T`, or `B`.
- Groups are not valid edge endpoints. Do not write `{group}` on an edge to a service (it fails).

### Layout control (works in the bundled VS Code renderer)
- `align row a b c` puts nodes in one horizontal row. Edges between aligned nodes become straight lines.
- `align column a b` puts nodes in one vertical column.
- Build a grid: one `align row` per tier, then connect neighbours. This fixed the layout in `13-complex-system-logos.md`.
- Keep most edges within a row or to the row below. Long or backward edges cause crossings.
- Remove duplicate edges. Each extra edge pulls nodes out of place.
- Config knobs (frontmatter `config: architecture:`), which the bundled renderer reads:
  - `nodeSeparation` (default 75)
  - `edgeElasticity` (default 0.45)
  - `randomize` (default false)
  - `idealEdgeLengthMultiplier` (default 1.5). Applies only to same-group edges, so it does not help cross-group edges.
  - Use these only as a fallback. `align` and fewer edges fix more.

### Icons
- Built-in names: `cloud`, `database`, `disk`, `internet`, `server`.
- Logo packs bundled with VS Code's Mermaid preview: `logos:` (719 icons) and `mdi:` (6573 icons). No install needed. Use the `name:icon` form.
- Verified `logos` names: `aws-cloudfront`, `aws-waf`, `aws-api-gateway`, `auth0-icon`, `aws-eks`, `spring-icon`, `nodejs-icon`, `kafka-icon`, `aws-elasticache`, `aws-redshift`, `aws-aurora`, `mongodb-icon`, `aws-s3`, `apache-spark`, `airflow-icon`, `opentelemetry-icon`, `github-icon`, `terraform-icon`, `argo-icon`.
- Verified `mdi` names: `language-python`, `database-search`, `chart-line`, `view-dashboard`, `eye-outline`.
- Not in the bundled `logos` pack (do not use): `keycloak`, `apache-airflow`, `java`, `python`, `redis`, `postgresql`, `elasticsearch`, `grafana`, `prometheus`, plain `opentelemetry`, plain `kafka`.
- Missing logo: use the closest `logos` icon or a generic `mdi` icon, and say so in the Legend.
- Check a new name with exact-match extraction from `/usr/share/code/resources/app/extensions/mermaid-markdown-features/markdown-preview-out/logos-*.js` or `mdi-*.js` (Linux path). Do not use `tr` to strip characters, because it removes letters from names.

### Known version note
- The bundled extension's `package.json` says Mermaid 10.0.0, but its architecture renderer includes `align` and the layout keys. Trust the bundle over the version string. Test any new feature in the preview before relying on it.

## UML to Mermaid cheatsheet

Fit levels come from the repo's `diagrams/uml/` files.

| UML diagram | Mermaid | Fit | Quick syntax |
|---|---|---|---|
| Class | `classDiagram` | Native | `class X { +op() }`, `A "1" --> "*" B : label`, `A <\|.. B` (realization), `A o-- B` (aggregation), `A *-- B` (composition), `<<interface>>` |
| Object | `flowchart` | Approximate | Nodes labelled `obj: Class` with attribute lines |
| Component | `flowchart` | Approximate | `subgraph` as component, `[(db)]` for a database, `-->\|label\|` for interfaces |
| Composite structure | `flowchart` | Approximate | Nested `subgraph` for parts and ports |
| Deployment | `flowchart` | Approximate | `subgraph` for node and execution environment, artifact nodes inside, `-->\|TLS 1433\|` for protocols |
| Package | `flowchart` | Close | `subgraph` per package, `-.->` dependency or `-->` |
| Activity | `flowchart` | Close | `([start])`, `{decision}`, `[action]`, `-->\|guard\|`, `subgraph` for swimlanes |
| Sequence | `sequenceDiagram` | Native | `participant X as Name`, `A->>B: msg`, `A-->>B: reply`, `alt/else/end`, `loop`, `par` |
| Use case | `flowchart` | Approximate | Actors as nodes, use cases as `([rounded])`, `subgraph` for system boundary |
| State machine | `stateDiagram-v2` | Native | `[*] --> S`, `S --> T : event`, `state X { ... }`, `state c <<choice>>` |
| Communication | `flowchart` | Approximate | Objects as nodes, numbered messages `1: call()` on edges |
| Interaction overview | `flowchart` | Close | Activity-style flow where nodes can be `[[subdiagram]]` |
| Timing | none | Not supported | Use PlantUML `concise` or `robust` |
| Profile | `classDiagram` | Approximate | `<<stereotype>>` classes and tagged values in notes |

Flowchart shape reference:
- `A[rect]`, `A(rounded)`, `A([stadium])`, `A{decision}`, `A[(database)]`, `A((circle))`, `A[[subroutine]]`
- Edge styles: `-->` solid, `-.->` dotted, `==>` thick, `-->|label|` labelled

## Style rules
- Only comment code that needs clarification. In diagrams this means keeping labels short and putting detail in the Legend.
- Title, one-line description, "Mermaid type" note, diagram, Legend, Notes. Match `diagrams/architecture/01-cloud-architecture.md`.
- Use `#` for the file title and `##` for sections.

## Checklist before done
- [ ] Diagram type matches the decision table
- [ ] Every icon name exists in the bundled packs
- [ ] No `{group}` on service edges, no groups as edge endpoints
- [ ] Each tier uses `align row`, edges mostly connect neighbours
- [ ] No duplicate edges
- [ ] Legend lists every non-built-in icon and any substitutions
- [ ] Temp files removed, nothing installed

---
name: sdlc-design
description: "AI-SDLC prompts for Solution design. Use it when design is needed before implementation: solution design, Mermaid diagrams, use cases, ADRs (architecture decisions), API contract, API versioning and deprecation, or data model."
license: CC-BY-4.0
---

# AI-SDLC phase 04 — Solution design

This skill groups the prompts of the **Solution design** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 4.1 — Functional and technical solution design
- File: [references/04-01-diseno-solucion.md](references/04-01-diseno-solucion.md)
- When to use it: once functional, technical and impact analysis is complete, before planning or executing any change.
- Inputs: completed functional, technical, and cross-impact analysis (`02-01`, `02-02`, `02-03`), existing architecture and contracts
- Permitted autonomy: A1 — Propose
- Stop if: if there is no viable rollback strategy for a critical component, state it as an open risk in the design instead of omitting it
- Next: `05-01-plan-implementacion` (skill `sdlc-planning`), `04-02-diagramas-mermaid`, `04-06-diseno-contrato-api`, `04-07-diseno-modelo-datos`

### 4.2 — Generate Mermaid diagrams
- File: [references/04-02-diagramas-mermaid.md](references/04-02-diagramas-mermaid.md)
- When to use it: during or after solution design (`04-01`), to document and visually communicate the changes.
- Inputs: approved design (`04-01`), real system architecture, source code or components involved in the change
- Permitted autonomy: A0 — Analyze the existing design and code; A1 — Propose the diagrams as a documentation artifact
- Stop if: stop if there is no approved design (`04-01`) to derive the diagrams from; never invent components, actors, or flows that do not exist in the real code or design
- Next: `04-03-casos-de-uso`

### 4.3 — Use case design
- File: [references/04-03-casos-de-uso.md](references/04-03-casos-de-uso.md)
- When to use it: during the design phase, to formalize the expected system behavior before implementing.
- Inputs: prior functional analysis (`02-01`), existing use-case documentation, target module or functionality
- Permitted autonomy: A1 — Propose
- Stop if: if business rules, postconditions, or verifiable acceptance criteria are missing for a flow, mark it as pending functional validation instead of inventing them
- Next: `04-04-adr-decisiones-arquitectura`, `05-01-plan-implementacion` (skill `sdlc-planning`)

### 4.4 — Architecture Decision Records (ADR)
- File: [references/04-04-adr-decisiones-arquitectura.md](references/04-04-adr-decisiones-arquitectura.md)
- When to use it: when making a significant architectural decision (technology choice, design pattern, integration strategy, data structure), when documenting past decisions that were not recorded, or as a review at the beginning of a project.
- Inputs: problem context, evaluated options, decision already made (this prompt documents, it does not decide)
- Permitted autonomy: A1 — Propose
- Stop if: before assigning the number, check `docs/decisions/README.md` or the existing index to avoid colliding with an already-used ADR-NNN
- Next: `05-01-plan-implementacion` (skill `sdlc-planning`)

### 4.5 — API Versioning and Deprecation
- File: [references/04-05-versionado-deprecacion-api.md](references/04-05-versionado-deprecacion-api.md)
- When to use it: when a change to an API breaks (or may break) the existing contract with its consumers — renaming/removing fields, changing types, modifying authentication, changing status codes or the semantics of an endpoint — and you need to decide how to introduce it without leaving clients unaware.
- Inputs: affected endpoint(s) or operation, nature of the proposed change, known consumers of the API (internal/external, if known), the project's existing versioning policy (if any), current SLA or support agreements with consumers
- Permitted autonomy: A1 — Propose
- Stop if: stop and escalate if it cannot be determined whether the change is breaking or not; stop if the consumer base is entirely unknown and the prompt cannot explicitly flag that gap; never propose removing a version without a defined notice period
- Next: `09-06-coordinacion-breaking-changes` (skill `sdlc-integration`)

### 4.6 — API contract design: endpoints, schemas, and interface semantics
- File: [references/04-06-diseno-contrato-api.md](references/04-06-diseno-contrato-api.md)
- When to use it: after the solution design (`04-01`) when it exposes a new API, or as a standalone step when the requirement is explicitly to design an interface.
- Inputs: related solution design (`04-01`) if it exists, related use cases (`04-03`) if they exist, intended consumers (internal/external), API style (REST/GraphQL/gRPC/other), existing project conventions if any
- Permitted autonomy: A1 — Propose
- Stop if: if the API style (REST/GraphQL/gRPC) is not defined and cannot be inferred from existing project conventions, ask before assuming one; no operation may be left without its error matrix defined
- Next: `04-05-versionado-deprecacion-api`, `05-01-plan-implementacion` (skill `sdlc-planning`), `07-02-pruebas-integracion` (skill `sdlc-testing`)

### 4.7 — Detailed data model design: entities, relationships, and schema
- File: [references/04-07-diseno-modelo-datos.md](references/04-07-diseno-modelo-datos.md)
- When to use it: during the design phase (after `04-01`, in parallel with or after `04-03`), when the change or project requires a new data model or a significant extension of the existing one — before writing the actual migration.
- Inputs: domain entities and relationships (or the solution design `04-01` / use cases `04-03` to infer them from), database engine (relational/document/other), expected volume and access pattern (reads vs.
- Permitted autonomy: A1 — Propose
- Stop if: if the database engine or the expected access pattern is unknown, stop and request it before proposing a schema — normalization and indexing strategy depend directly on that information
- Next: `08-05-revision-migracion-esquema-bd` (skill `sdlc-review`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

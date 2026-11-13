---
name: sdlc-documentation
description: "AI-SDLC prompts for Documentation. Use it when documentation is needed: technical docs, project technical record, release notes and CHANGELOG, observability and instrumentation, public API docs, or rollout training materials."
license: CC-BY-4.0
---

# AI-SDLC phase 10 — Documentation

This skill groups the prompts of the **Documentation** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 10.1 — Update technical documentation
- File: [references/10-01-documentacion-tecnica.md](references/10-01-documentacion-tecnica.md)
- When to use it: at the close of each change, before merging to the main branch.
- Inputs: reference issue or requirement, integrated branch, modified components, existing documents to review (README, docs/, architecture, API contracts)
- Permitted autonomy: A1 — Propose: delivers the list of documents to update with proposed content, without applying the change
- Stop if: if the actual change or modified components are unclear, it must request that information instead of proposing invented content
- Next: `10-02-memoria-tecnica`, `10-03-release-changelog`

### 10.2 — Technical memory of the change
- File: [references/10-02-memoria-tecnica.md](references/10-02-memoria-tecnica.md)
- When to use it: at the close of each issue or sprint, as a formal record of the work performed for audit and future reference.
- Inputs: issue or requirement, integrated branch, environment, modified components, commits/PRs, approved design, executed test results
- Permitted autonomy: A1 — Propose: drafts the technical memory document; does not publish or archive it itself
- Stop if: if test results are missing or the approved design is unavailable, it must flag that explicitly in the relevant section instead of inventing results
- Next: `10-03-release-changelog`, `11-03-deuda-tecnica` (skill `sdlc-operations`)

### 10.3 — Release or changelog documentation
- File: [references/10-03-release-changelog.md](references/10-03-release-changelog.md)
- When to use it: when preparing a release or closing a sprint to document delivered changes.
- Inputs: version or tag, release branch, included issues or PRs, commits of the period
- Permitted autonomy: A1 — Propose: delivers the changelog ready to publish; the actual publication in GitHub Releases or CHANGELOG.md is a separate, explicit A3 action
- Stop if: if it detects breaking changes without a clear migration note, it must stop and request that information before treating the changelog as complete
- Next: `10-02-memoria-tecnica`, `09-04-promotion-checklist` (skill `sdlc-integration`)

### 10.4 — Observability: Instrumentation and Monitoring
- File: [references/10-04-observabilidad-instrumentacion.md](references/10-04-observabilidad-instrumentacion.md)
- When to use it: Prompt to design and implement an application observability strategy: metrics, structured logs, and distributed traces pillars; alerts, dashboards, SLOs/SLAs, and signal correlation to detect and diagnose production problems.
- Inputs: technology stack, infrastructure, current observability stack, number of services, SLAs committed to customers, target environment; optionally a result from `13-04` (threat modeling)
- Permitted autonomy: A1 — Propose: catalog of SLOs, alerts, and dashboards; actual code instrumentation and deployment of agents/exporters requires A2 in an isolated workspace or branch with subsequent review
- Stop if: if there are no SLAs or business objectives defined to set the SLOs, it must flag this instead of inventing thresholds; it must not propose instrumentation that logs passwords, tokens, or unanonymized PII
- Next: `11-05-performance-produccion-diagnostico` (skill `sdlc-operations`), `11-04-incident-response` (skill `sdlc-operations`)

### 10.5 — Public API documentation for external developers
- File: [references/10-05-documentacion-api-publica.md](references/10-05-documentacion-api-publica.md)
- When to use it: after the API contract is already designed (`04-06`) and implemented, before exposing it to external consumers (partners, customers, third parties).
- Inputs: already implemented API contract (reference to `04-06` or real specification), target audience (external developers/partners/customers), real usage examples if available
- Permitted autonomy: A1 — Propose
- Stop if: if the behavior to be documented cannot be verified against the real implementation (the design contract has drifted from the code), stop and flag the discrepancy instead of documenting the theoretical design as if it were real behavior
- Next: `10-03-release-changelog`

### 10.6 — End-user training materials and rollout plan
- File: [references/10-06-materiales-capacitacion-rollout.md](references/10-06-materiales-capacitacion-rollout.md)
- When to use it: before launching a new feature or system to its non-technical end users, especially when it changes an existing workflow or affects a large user group.
- Inputs: description of the feature or system being launched, end-user audience (roles, technical level, approximate group size), available communication channel, launch date
- Permitted autonomy: A1 — Propose
- Stop if: if the technical level or audience size is unknown, stop and request it before proposing the training format — a short video and a written guide don't work the same for 5 expert users as for 500 non-technical ones
- Next: `17-06-reporte-estado-stakeholders` (skill `sdlc-engineering-backoffice`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

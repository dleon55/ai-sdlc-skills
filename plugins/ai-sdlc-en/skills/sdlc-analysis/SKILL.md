---
name: sdlc-analysis
description: "AI-SDLC prompts for Requirements and issue analysis. Use it when asked to analyze an issue, requirement or change: functional scope, technical analysis, cross-impact, stakeholder elicitation, non-functional requirements, GitHub backlog triage or a traceability matrix."
license: CC-BY-4.0
---

# AI-SDLC phase 02 — Requirements and issue analysis

This skill groups the prompts of the **Requirements and issue analysis** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 2.0 — Stakeholder requirements elicitation
- File: [references/02-00-elicitacion-requerimientos-stakeholders.md](references/02-00-elicitacion-requerimientos-stakeholders.md)
- When to use it: at the start of a new initiative, when only a vague idea or a business complaint exists, before a formally written issue or requirement exists.
- Inputs: initiative context (raw idea, complaint, or initial need), stakeholder role(s) to interview, transcript or notes of the conversation if it already happened (or "session not yet held" if the script is requested beforehand), initiative's business objective (or…
- Permitted autonomy: A0 — Analyze (synthesis of a conversation that already happened); A1 — Propose (interview script, probing questions)
- Stop if: if the transcript or notes do not allow distinguishing a real need from a solution already assumed by the stakeholder, state it explicitly instead of accepting the proposed solution as the requirement; if the stakeholder's role or another datum needed for the script is missing, request it instead o…
- Next: `02-05-analisis-integral-requerimientos`, `02-01-analisis-issue`

### 2.1 — Functional analysis of a requirement, issue or change
- File: [references/02-01-analisis-issue.md](references/02-01-analisis-issue.md)
- When to use it: as the first step when receiving a task, before any technical analysis or design.
- Inputs: issue or requirement to analyze, repository, module or functionality, workspace/subproject, and applicable standard/compliance
- Permitted autonomy: A0 — Analyze
- Stop if: if the issue does not provide enough information to fix expected behavior or acceptance criteria, state the gap and lower the `confidence_score` instead of inventing the scope
- Next: `02-02-analisis-tecnico`

### 2.2 - Deep technical analysis of existing code
- File: [references/02-02-analisis-tecnico.md](references/02-02-analisis-tecnico.md)
- When to use it: after functional analysis (`02-01`) and before cross-impact analysis (`02-03`) and solution design (`04-01`).
- Inputs: output of `02-01`, repository or workspace, issue or requirement, target branch or commit, environment, documents and contracts to review
- Permitted autonomy: A0 — Analyze
- Stop if: if behavior cannot be verified at runtime, label it as static analysis; if the JSON metadata `status` is `blocked`, stop and escalate instead of forcing conclusions
- Next: `02-03-impacto-cruzado`

### 2.3 — Cross-impact analysis
- File: [references/02-03-impacto-cruzado.md](references/02-03-impacto-cruzado.md)
- When to use it: after deep technical analysis (`02-02`) and before solution design (`04-01`).
- Inputs: output of `02-02` (technical flow and dependencies), architecture, API contracts, database schema, involved components
- Permitted autonomy: A0 — Analyze
- Stop if: if there is not enough evidence to rule out impact on a critical component (security, data, production, semver), classify it as an unconfirmed high risk instead of omitting it from the matrix
- Next: `04-01-diseno-solucion` (skill `sdlc-design`)

### 2.4 — GitHub Issues backlog triage and planning
- File: [references/02-04-triage-backlog-github.md](references/02-04-triage-backlog-github.md)
- When to use it: when you need to review open or pending issues as a work portfolio, order their attention by priority or component, or prepare a master execution plan for a sprint, remediation, or stabilization effort.
- Inputs: issues source (e.g., `gh issue list` JSON output), applied filter, pending backlog criteria, target component or owner, target branch and environment, documents to review
- Permitted autonomy: A1 — Propose
- Stop if: do not propose closing issues without evidence; if an issue's information is not enough to classify it precisely, state it as an assumption and lower the confidence level instead of assigning it a definitive priority
- Next: `05-01-plan-implementacion` (skill `sdlc-planning`), `02-01-analisis-issue`

### 2.5 — Comprehensive Requirement Analysis and Issue Generation (PRO)
- File: [references/02-05-analisis-integral-requerimientos.md](references/02-05-analisis-integral-requerimientos.md)
- When to use it: when receiving a complex user requirement, a change request (CR), or a product idea that has not yet been technically formalized.
- Inputs: user_requirement (an idea or CR not yet formalized), repository, base_branch, existing related documentation and code
- Permitted autonomy: A1 — Propose
- Stop if: if Definition of Ready compliance cannot be confirmed (acceptance criteria, scope, or impact not verifiable), mark the resulting issue as "not ready" instead of presenting it as Ready
- Next: `02-04-triage-backlog-github`, `04-01-diseno-solucion` (skill `sdlc-design`), `02-07-matriz-trazabilidad-requerimientos`

### 2.6 — Non-functional requirements specification
- File: [references/02-06-requerimientos-no-funcionales.md](references/02-06-requerimientos-no-funcionales.md)
- When to use it: after functional requirements are defined (`02-05`) or the tentative architecture exists (`00-D-02`), and before solution design (`04-01`) — NFRs condition design decisions that are expensive to reverse if discovered late.
- Inputs: system or change context, functional requirements already defined (from `02-05`/`04-03`) if they exist, known business constraints (contractual SLA, compliance, infrastructure budget), tentative architecture or stack if it exists (`00-D-02`)
- Permitted autonomy: A0 — Analyze (catalog NFRs already stated or inferable from context); A1 — Propose (suggested thresholds when the business hasn't set them, always explicitly marked as a proposal to validate)
- Stop if: if an NFR cannot be expressed with a measurable threshold (number, unit, test condition), do not declare it as defined — register it as "pending quantification" instead of inventing a figure
- Next: `04-01-diseno-solucion` (skill `sdlc-design`), `07-06-pruebas-performance-carga` (skill `sdlc-testing`)

### 2.7 — Whole-project requirements traceability matrix
- File: [references/02-07-matriz-trazabilidad-requerimientos.md](references/02-07-matriz-trazabilidad-requerimientos.md)
- When to use it: periodically during the execution of a project with multiple requirements already analyzed (`02-05`), to detect orphaned requirements (missing design, code, or test) or code with no formal requirement backing it, before the project is considered closed.
- Inputs: list of the project's business requirements (or issues already analyzed with `02-05`), associated designs, related implementations/PRs, available test results
- Permitted autonomy: A0 — Analyze (aggregate already-evidenceable traceability); A1 — Propose (flag and prioritize gaps)
- Stop if: if a requirement cannot be linked to any design, code, or test evidence, do not mark it as "covered" — explicitly report it as orphaned
- Next: `08-01-revision-completa-pr` (skill `sdlc-review`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

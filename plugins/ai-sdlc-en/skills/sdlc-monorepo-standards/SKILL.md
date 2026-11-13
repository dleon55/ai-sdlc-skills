---
name: sdlc-monorepo-standards
description: "AI-SDLC prompts for Monorepo and quality standards. Use it when working on a monorepo (workspaces and dependencies) or measuring quality and compliance with PSP/TSP, ISO or MoProSoft."
license: CC-BY-4.0
---

# AI-SDLC phase 14 — Monorepo and quality standards

This skill groups the prompts of the **Monorepo and quality standards** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 14.1 — Dependency and workspace auditing in monorepos
- File: [references/14-01-monorepo-workspaces-dependencias.md](references/14-01-monorepo-workspaces-dependencias.md)
- When to use it: at the beginning of a major technical change or refactoring that affects shared libraries (`packages/`, `shared/`) inside a monorepo.
- Inputs: source workspace/subproject to analyze, monorepo configuration files (package.json, pnpm-workspace.yaml, go.work, lerna.json, turbo.json, tsconfig.json)
- Permitted autonomy: A0 — Analyze
- Stop if: if the monorepo configuration files are not accessible or are ambiguous, state the graph as incomplete instead of assuming unverified dependency relationships
- Next: `05-01-plan-implementacion` (skill `sdlc-planning`), `04-04-adr-decisiones-arquitectura` (skill `sdlc-design`)

### 14.2 — Quality metrics logging and PSP/TSP estimations
- File: [references/14-02-psp-tsp-metricas-calidad.md](references/14-02-psp-tsp-metricas-calidad.md)
- When to use it: at the beginning of development to record the base estimation (plan) and at the end of each software engineering phase to record actual effort and defects.
- Inputs: current issue or requirement, cycle phase (Planning, Design, Coding, Code Review, Testing, Post-mortem), previous metrics or log if they exist
- Permitted autonomy: A0 — Analyze the current status; A1 — Propose the updated log of estimates and actual metrics
- Stop if: do not invent actual times or defects not reported by the developer; if the base estimate (plan) for a phase is missing, request it before calculating yield or defect density
- Next: `14-03-iso-moprosoft-compliance`

### 14.3 — ISO 29110 / MOPROSOFT process compliance audit
- File: [references/14-03-iso-moprosoft-compliance.md](references/14-03-iso-moprosoft-compliance.md)
- When to use it: before deployment to controlled environments (Staging / Prod), as part of the quality gates in the release process.
- Inputs: workspace/subproject and compliance standard to audit (ISO 29110 / MOPROSOFT / MAAGTICSI), generated artifacts (Implementation Plan, Test Cases, Test Code, Technical Memory), information security evidence (SAST/DAST report or applicable policy) if the ISO 270…
- Permitted autonomy: A0 — Analyze the conformity of each artifact; A1 — Propose the verdict and the mandatory remediation actions
- Stop if: do not issue an "Approved" verdict if bidirectional requirement-design-code-test traceability is missing; mark as "Rejected" or "Approved with Reservations" for any non-conformity without evidence of mitigation
- Next: `08-03-remediacion-maestro` (skill `sdlc-review`), `09-04-promotion-checklist` (skill `sdlc-integration`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

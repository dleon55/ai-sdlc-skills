---
name: sdlc-review
description: "AI-SDLC prompts for Code and PR review. Use it when asked to review a full pull request, plan remediation of findings, profile SQL queries or review a database schema migration."
license: CC-BY-4.0
---

# AI-SDLC phase 08 — Code and PR review

This skill groups the prompts of the **Code and PR review** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 8.1 — Complete PR Review: Quality, Compliance, and Integration
- File: [references/08-01-revision-completa-pr.md](references/08-01-revision-completa-pr.md)
- When to use it: after implementing changes and before merging any PR — the complete review step before merge, in a single prompt instead of several separate invocations.
- Inputs: the PR's real diff, associated issue/requirement, approved design if any, test results, commit history and related active branches, local and GitHub Actions CI logs, project code standards
- Permitted autonomy: A1 — Propose (the verdict and integration strategy are proposed; executing the merge, applying remediation, or resolving conflicts requires a separate execution prompt and human approval)
- Stop if: if the full diff, the original requirement, or any of the four compliance inputs (requested/designed/implemented/tested) is missing, declare the evidence gap in that specific dimension instead of omitting it or assuming it's fine; if local state isn't synced with remote, sync (`git fetch`) before e…
- Next: `08-03-remediacion-maestro`, `09-04-promotion-checklist` (skill `sdlc-integration`)

### 8.3 — Static review remediation (master prompt)
- File: [references/08-03-remediacion-maestro.md](references/08-03-remediacion-maestro.md)
- When to use it: when a static review report is received and a structured correction plan is needed, not just superficial patches.
- Inputs: static review report with critical, medium, and minor findings
- Permitted autonomy: A1 — Propose (block 1); A2 — Execute controlled (block 2, only after human approval of block 1's plan)
- Stop if: do not start the execution block without explicit approval of the analysis plan; stop if a proposed change affects system stability without a clear mitigation
- Next: `07-01-pruebas-unitarias` (skill `sdlc-testing`), `07-02-pruebas-integracion` (skill `sdlc-testing`)

### 8.4 — SQL Execution Plan Audit and Profiling (DBA)
- File: [references/08-04-sql-query-profiling.md](references/08-04-sql-query-profiling.md)
- When to use it: When an endpoint or service exhibits slowness (high latency) in production, or during the review of PRs that introduce complex database queries.
- Inputs: `EXPLAIN ANALYZE` output or ORM log, DDL or models of the relevant schema, database engine used
- Permitted autonomy: A1 — Propose (delivers diagnosis, optimized query and index DDL as a proposal; does not execute them)
- Stop if: if the schema or execution plan lacks real table volumetry or up-to-date statistics, present the diagnosis as preliminary and do not guarantee the estimated impact
- Next: `08-01-revision-completa-pr`

### 8.5 — Database Schema Migration Review
- File: [references/08-05-revision-migracion-esquema-bd.md](references/08-05-revision-migracion-esquema-bd.md)
- When to use it: before running a schema migration against staging or production — as part of the PR that introduces the migration file, or as a final gate before `migrate up` in the deployment pipeline.
- Inputs: migration script or file (exact DDL, up and down if they exist), database engine and version, approximate size and traffic of the affected table(s), relevant fragment of the currently deployed code that reads or writes those columns/tables, deployment strateg…
- Permitted autonomy: A0 — Analyze (risk diagnosis); A1 — Propose (corrected migration version, expand-contract plan, rollback script, as a proposal); never A2/A3 — this prompt never executes or applies the migration under any circumstance
- Stop if: stop and escalate to explicit human approval if the migration acquires a full table lock on a high-traffic table without a maintenance-window plan; stop if compatibility with the currently deployed code cannot be confirmed; never treat an irreversible data-loss operation as acceptable just because…
- Next: `11-09-runbook-rollback` (skill `sdlc-operations`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

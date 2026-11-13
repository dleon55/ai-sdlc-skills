---
name: sdlc-incidents
description: "AI-SDLC prompts for Incidents and root cause. Use it when there is a bug, failure or incident reported on GitHub that needs investigating: reproduction, evidence, root cause analysis (RCA) and a proposed fix."
license: CC-BY-4.0
---

# AI-SDLC phase 03 — Incidents and root cause

This skill groups the prompts of the **Incidents and root cause** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 3.1 — Review of incidents reported by tester against GitHub Issues
- File: [references/03-01-incidentes-github.md](references/03-01-incidentes-github.md)
- When to use it: when receiving a QA cycle report, before managing any defect in GitHub.
- Inputs: normalized QA incident report, read access to open and closed GitHub issues
- Permitted autonomy: A1 — Propose (drafts issues and actions, does not execute them)
- Stop if: the prompt itself explicitly restricts its scope to analysis and drafting; never run mutation actions on GitHub
- Next: `03-02-causa-raiz`

### 3.2 — Root cause analysis
- File: [references/03-02-causa-raiz.md](references/03-02-causa-raiz.md)
- When to use it: when investigating defects in QA or production, when the symptom is clear but the cause is not.
- Inputs: logs, code, configurations, recent commits and deployments; reference issue or incident
- Permitted autonomy: A0 — Analyze
- Stop if: if the root cause cannot be confirmed, state confidence level and missing evidence instead of forcing a conclusion
- Next: `05-01-plan-implementacion` (skill `sdlc-planning`), `08-03-remediacion-maestro` (skill `sdlc-review`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

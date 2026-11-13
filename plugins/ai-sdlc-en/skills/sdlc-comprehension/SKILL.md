---
name: sdlc-comprehension
description: "AI-SDLC prompts for Repository and process comprehension. Use it when you need to understand an existing repository or system before changing it: onboarding and code map, modules, dependencies, flows and the business processes it implements."
license: CC-BY-4.0
---

# AI-SDLC phase 01 — Repository and process comprehension

This skill groups the prompts of the **Repository and process comprehension** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 1.1 — Repository technical inventory
- File: [references/01-01-arranque-comprension-repositorio.md](references/01-01-arranque-comprension-repositorio.md)
- When to use it: when starting work on a repository with no prior context, or to refresh the inventory after significant structural changes.
- Inputs: read access to the complete repository (source code, configuration, existing documentation); no reference issue or incident required
- Permitted autonomy: A0 — Analyze
- Stop if: if parts of the repository are inaccessible or the monorepo has unresolved workspaces, state the covered scope and gaps instead of inferring unverified structure
- Next: `01-02-analisis-procesos`, `02-01-analisis-issue` (skill `sdlc-analysis`)

### 1.2 — Locate processes, procedures and project policies
- File: [references/01-02-analisis-procesos.md](references/01-02-analisis-procesos.md)
- When to use it: before any analysis or implementation work, to understand the project governance framework and avoid violating already defined rules.
- Inputs: read access to README, docs/, exported wiki, ADRs, contribution files, and workflows in the repository
- Permitted autonomy: A0 — Analyze
- Stop if: if no documentary evidence is found for a governance category (e.g., security or branching), state it as "does not exist" instead of assuming an implicit policy
- Next: `01-01-arranque-comprension-repositorio`, `02-01-analisis-issue` (skill `sdlc-analysis`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

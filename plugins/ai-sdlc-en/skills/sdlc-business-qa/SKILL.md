---
name: sdlc-business-qa
description: "AI-SDLC prompts for Business and functional QA. Use it when writing user stories with Gherkin, manual test cases, or analyzing defects from a business point of view."
license: CC-BY-4.0
---

# AI-SDLC phase 15 — Business and functional QA

This skill groups the prompts of the **Business and functional QA** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 15.1 — User stories and Gherkin acceptance criteria
- File: [references/15-01-historias-usuario-gherkin.md](references/15-01-historias-usuario-gherkin.md)
- When to use it: Prompt for business analysts and product owners. Converts raw business requests and requirements into structured user stories and incorporates acceptance criteria in Gherkin format (Given / When / Then).
- Inputs: business requirement or request to convert, affected module or process, applicable compliance standard if any (ISO 29110 / MOPROSOFT)
- Permitted autonomy: A1 — Propose the user stories and acceptance criteria as a documentation artifact
- Stop if: do not invent business rules, roles, or flows that are not implied by the original request; if the requirement is ambiguous, state the assumptions used instead of silently assuming
- Next: `04-01-diseno-solucion` (skill `sdlc-design`), `15-02-casos-prueba-manuales`

### 15.2 — Design of manual and functional test cases
- File: [references/15-02-casos-prueba-manuales.md](references/15-02-casos-prueba-manuales.md)
- When to use it: Prompt for manual testers and functional QAs. Generates detailed manual test cases (step-by-step, test data, expected results) from user stories or functional specifications without requiring programming skills.
- Inputs: user story or requirement to validate, acceptance criteria or business rules if they exist (ideally from `15-01`)
- Permitted autonomy: A1 — Propose the manual test case suite as an artifact ready for QA execution
- Stop if: do not invent business rules or system behaviors not described in the requirement; if acceptance criteria are missing, state this and limit coverage to what is verifiable with the available information
- Next: `07-05-automatizacion-antigravity` (skill `sdlc-testing`), `07-03-pruebas-e2e` (skill `sdlc-testing`)

### 15.3 — Defect reporting and business impact analysis
- File: [references/15-03-analisis-defectos-negocio.md](references/15-03-analisis-defectos-negocio.md)
- When to use it: Prompt for manual testers and functional analysts. Helps structure professional bug reports, translating technical errors (console messages, failed HTTP responses) into business consequences and user impact, facilitating prioritization by the development team.
- Inputs: description of the observed error, steps performed, expected behavior, technical evidence if available (log, HTTP code, screenshot)
- Permitted autonomy: A1 — Propose
- Stop if: if technical severity and business priority cannot be justified from the given evidence, state that instead of assuming an impact level
- Next: `03-01-incidentes-github` (skill `sdlc-incidents`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

---
name: sdlc-planning
description: "AI-SDLC prompts for Implementation planning. Use it when an approved design must be turned into a step-by-step implementation plan or when assessing the risks of implementing it."
license: CC-BY-4.0
---

# AI-SDLC phase 05 — Implementation planning

This skill groups the prompts of the **Implementation planning** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 5.1 — Detailed implementation plan
- File: [references/05-01-plan-implementacion.md](references/05-01-plan-implementacion.md)
- When to use it: after approved design (`04-01`), before executing any change in the repository.
- Inputs: approved design (`04-01`), architecture, contracts, target branch, target environment, components to modify
- Permitted autonomy: A1 — Propose (plan or artifact without applying it); does not by itself authorize executing, committing, or deploying
- Stop if: stop if there is no approved design to start from; do not leave any step without defined expected evidence, dependency, or risk; explicitly flag any step that requires a production environment
- Next: `05-02-riesgos-implementacion`, `06-01-implementacion-multiagente` (skill `sdlc-implementation`), `07-00-deteccion-stack-pruebas` (skill `sdlc-testing`)

### 5.2 — Implementation risk and impact analysis
- File: [references/05-02-riesgos-implementacion.md](references/05-02-riesgos-implementacion.md)
- When to use it: in parallel with the implementation plan (`05-01`), before executing any change.
- Inputs: approved design, architecture, incident history, implementation plan (`05-01`) in progress or approved
- Permitted autonomy: A0 — Analyze risks and potential impact; A1 — Propose the risk matrix with mitigation and contingency
- Stop if: stop if there is no reference design or plan; escalate to human review before moving on to `06-01` if any risk remains classified as high without a viable mitigation
- Next: `06-01-implementacion-multiagente` (skill `sdlc-implementation`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

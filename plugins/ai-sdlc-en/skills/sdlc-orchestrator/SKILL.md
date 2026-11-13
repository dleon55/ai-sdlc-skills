---
name: sdlc-orchestrator
description: "AI-SDLC prompts for Full-cycle orchestrator. Use it when a large assignment needs several phases, capabilities or agents coordinated and you must choose the minimum sufficient flow; for a simple task use the phase skill directly."
license: CC-BY-4.0
---

# AI-SDLC phase 12 — Full-cycle orchestrator

This skill groups the prompts of the **Full-cycle orchestrator** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 12 — Master orchestrator prompt for complete cycle
- File: [references/12-orquestador.md](references/12-orquestador.md)
- When to use it: when an assignment requires coordination across capabilities, phases, or agents. For simple tasks, use the specialized prompt directly.
- Inputs: issue/requirement, target branch, environment, components, permitted autonomy level, available tools, budget
- Permitted autonomy: dynamically defined by the prompt itself (Step 3, "Create contract"); must never exceed the declared input autonomy level nor the target prompt's own autonomy ceiling — whichever of the two is lower is granted
- Stop if: "Do not execute all phases by default"; escalate to a human when risk or permission exceeds the generated contract, or when the input autonomy exceeds the target prompt's own autonomy ceiling for a delegation

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

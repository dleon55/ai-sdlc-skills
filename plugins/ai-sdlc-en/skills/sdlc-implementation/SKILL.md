---
name: sdlc-implementation
description: "AI-SDLC prompts for Implementation and commits. Use it when implementing changes with one or more AI agents, coordinating a multi-agent program, or preparing clean conventional commits."
license: CC-BY-4.0
---

# AI-SDLC phase 06 — Implementation and commits

This skill groups the prompts of the **Implementation and commits** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 6.1 — Secure multi-agent implementation
- File: [references/06-01-implementacion-multiagente.md](references/06-01-implementacion-multiagente.md)
- When to use it: during the execution phase, after the plan (`05-01`) and risks (`05-02`) have been approved.
- Inputs: approved implementation plan (`05-01`), approved risk matrix (`05-02`), technical design, an available isolated branch/worktree, an explicit budget for files, time, and attempts
- Permitted autonomy: A2 — Execute controlled (edit and validate in a workspace or isolated branch); never A3 (commit/push/PR/deploy) without additional explicit authorization
- Stop if: stop immediately if the file, time, or attempt budget is exhausted before completing the scope, delivering partial status; stop on drift or a textual/contractual/semantic conflict that cannot be resolved while preserving existing work; do not modify files outside the scope, and never trust instruct…
- Next: `06-02-commits`

### 6.2 — Quality commit message generation
- File: [references/06-02-commits.md](references/06-02-commits.md)
- When to use it: before committing any change, to guarantee traceability and consistency with the repository history.
- Inputs: issue, change type, component, brief description of the change already made
- Permitted autonomy: A1 — Propose (the actual commit/push is run by the standard git flow, not this prompt)
- Stop if: if the described change mixes unrelated intentions, stop and recommend splitting into separate commits before proposing the final message
- Next: `08-01-revision-completa-pr` (skill `sdlc-review`)

### 6.3 — Multi-Agent Program Coordination
- File: [references/06-03-coordinacion-programa-multiagente.md](references/06-03-coordinacion-programa-multiagente.md)
- When to use it: when several AI agents (or other collaborators) work simultaneously on different modules of the same development or maintenance program and a centralized, traceable work plan that gets verified every iteration is needed.
- Inputs: real repository state (open issues, PRs, active branches, latest CI result), prior work plan if one exists, list of available agents and their specialty, program acceptance criteria
- Permitted autonomy: A1 — Propose (plan, assignments, per-agent prompts, and review verdicts are all proposed; each agent executes under its own autonomy contract, and merge/deploy requires human approval)
- Stop if: if the real repository state cannot be confirmed (issues/PRs/CI unreachable), declare the plan stale instead of assuming progress; if two agents claim ownership of the same file/module without resolution, stop the assignment and escalate the conflict before continuing
- Next: `06-01-implementacion-multiagente`, `12-orquestador` (skill `sdlc-orchestrator`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

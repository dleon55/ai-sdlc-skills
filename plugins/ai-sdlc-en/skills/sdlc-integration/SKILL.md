---
name: sdlc-integration
description: "AI-SDLC prompts for Continuous integration and delivery. Use it when working on CI/CD: GitHub Actions workflows, environment promotion checklist, feature flag strategy, or coordinating breaking changes."
license: CC-BY-4.0
---

# AI-SDLC phase 09 — Continuous integration and delivery

This skill groups the prompts of the **Continuous integration and delivery** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 9.3 — GitHub Actions workflows review
- File: [references/09-03-workflows-github-actions.md](references/09-03-workflows-github-actions.md)
- When to use it: periodically as pipeline health review, or when incorporating new modules or environments.
- Inputs: contents of `.github/workflows/`, CI/CD README
- Permitted autonomy: A0 — Analyze
- Stop if: if a workflow references secrets or permissions that cannot be inspected without access to the repository configuration, document it as a visibility gap instead of assuming its state
- Next: `11-02-hardening-seguridad` (skill `sdlc-operations`)

### 9.4 — Promotion checklist: integration and deployment between environments
- File: [references/09-04-promotion-checklist.md](references/09-04-promotion-checklist.md)
- When to use it: before any deployment to a higher environment, especially before going to production. Also useful to define the project's standard promotion process.
- Inputs: reference to the issue/PR, source branch, source and target environment, deployment stack, indication of whether there are DB migrations, infrastructure changes or environment variable changes
- Permitted autonomy: A1 — Propose (generates the checklist and the go/no-go semaphore; executing the deployment and rollback requires explicit A3 by the release owner)
- Stop if: if no rollback owner is available, if there are DB migrations without a confirmed backup, or if any explicit NO-GO condition from section 2 is met, stop and do not recommend proceeding with the deployment
- Next: `08-01-revision-completa-pr` (skill `sdlc-review`)

### 9.5 — Feature Flag / Kill-Switch Strategy
- File: [references/09-05-estrategia-feature-flags.md](references/09-05-estrategia-feature-flags.md)
- When to use it: when a change needs a progressive or controlled rollout instead of an all-at-once deployment — for example, a high-risk feature, a significant UX change, or a change to a critical business flow.
- Inputs: feature or change to flag, expected flag type (release/ops/experiment), feature flag platform, layers where it is evaluated (client/server/edge), whether there is an associated A/B experiment, target date or milestone for full rollout
- Permitted autonomy: A1 — Propose (complete strategy design without applying it); creating and enabling flags on the real platform requires explicit A2/A3 by the team that owns the feature
- Stop if: stop and escalate if the proposed kill-switch depends on the same deploy pipeline it is meant to bypass in an emergency; do not propose a rollout progression without measurable promotion/pause criteria; do not leave any flag without an owner or a removal plan
- Next: `09-06-coordinacion-breaking-changes`

### 9.6 — Cross-Team Breaking Change Coordination
- File: [references/09-06-coordinacion-breaking-changes.md](references/09-06-coordinacion-breaking-changes.md)
- When to use it: when a change breaks (or may break) a contract that other teams, services, or external consumers depend on, and the outbound communication needs coordinating before deployment — not just the technical design of the change.
- Inputs: an existing versioning/deprecation plan (from `04-05-versionado-deprecacion-api` or an equivalent document), the known list of teams/services/consumers that depend on the contract, the target cutover or release date, the communication channels available per a…
- Permitted autonomy: A1 — Propose (drafts the communication, the notice calendar, and the readiness checklist; actually sending the communication, escalating directly to a consumer, and deciding to proceed with the cutover require human or team-owner approval)
- Stop if: stop and escalate if the full list of affected consumers can't be confirmed — declare it incomplete rather than treating it as closed; stop if no minimum notice period per audience has been defined; never recommend proceeding with the cutover if a high-impact consumer hasn't explicitly confirmed re…
- Next: `09-04-promotion-checklist`

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

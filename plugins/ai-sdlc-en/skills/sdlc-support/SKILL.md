---
name: sdlc-support
description: "AI-SDLC prompts for Support and help desk. Use it for user support: ticket triage, diagnosing and answering a support incident, knowledge base articles, escalation matrix and SLA, ticket trends, or knowledge base audits."
license: CC-BY-4.0
---

# AI-SDLC phase 16 — Support and help desk

This skill groups the prompts of the **Support and help desk** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 16.1 — Support Ticket Triage and Classification
- File: [references/16-01-triage-tickets-soporte.md](references/16-01-triage-tickets-soporte.md)
- When to use it: when one or more new tickets arrive (support desk, help desk, customer incident channel) that need severity, SLA, and team assigned before anyone intervenes.
- Inputs: text and metadata of the ticket or batch of tickets (title, description, reporter, timestamp, environment, attachments/logs if any), current SLA table or policy by severity, read access to ticket history or a knowledge base to detect duplicates/known issues,…
- Permitted autonomy: A0 — Analyze (reading the ticket, searching for duplicates/known issues); A1 — Propose (proposed severity, SLA, and team); never A2/A3 — this prompt does not assign the ticket, change its status, or execute any action on the ticket system
- Stop if: stop and request more information if the ticket lacks enough data to determine severity (no description, no stated impact or environment) — never invent a plausible-looking severity; mark as "possible duplicate, unconfirmed" if the match with a prior ticket is unclear, instead of treating it as set…
- Next: `16-02-diagnostico-respuesta-incidente-soporte`, `11-04-incident-response` (skill `sdlc-operations`)

### 16.2 — Support Incident Diagnosis and First Response
- File: [references/16-02-diagnostico-respuesta-incidente-soporte.md](references/16-02-diagnostico-respuesta-incidente-soporte.md)
- When to use it: immediately after a ticket has been classified and prioritized by `16-01-triage-tickets-soporte`.
- Inputs: ticket already triaged with priority and severity assigned (output of `16-01`), reproduction steps reported by the user, affected environment, available evidence (logs, screenshots, error messages), read access to known incidents and the knowledge base, SLA o…
- Permitted autonomy: A0 — Analyze (diagnosis: reproduce, isolate probable cause, review KB); A1 — Propose (draft the first user response); never A2/A3 — this prompt does not execute or publish changes to the system
- Stop if: stop and escalate to an execution/engineering prompt (`03-01-incidentes-github` or `11-01-troubleshooting`) if the diagnosis confirms a code bug that requires a change; stop and escalate to `11-04-incident-response` if it is a production incident with significant impact; if the problem is not repro…
- Next: `16-01-triage-tickets-soporte`, `03-01-incidentes-github` (skill `sdlc-incidents`), `11-01-troubleshooting` (skill `sdlc-operations`), `11-04-incident-response` (skill `sdlc-operations`)

### 16.3 — Knowledge base article from a resolved ticket
- File: [references/16-03-articulo-base-conocimiento.md](references/16-03-articulo-base-conocimiento.md)
- When to use it: after a ticket is resolved and the pattern (symptom + cause + fix) is likely to recur, so the next support agent doesn't have to re-diagnose the same case from scratch.
- Inputs: resolved ticket with reported symptom, confirmed root cause (own or coming from the `16-02` diagnosis), applied and validated solution steps, affected system/product/version, target audience for the article
- Permitted autonomy: A1 — Propose (draft the KB article); never A2/A3 — publishing the article in the production KB system requires explicit human review and approval outside this prompt
- Stop if: stop and escalate if the ticket has no confirmed root cause (only a resolved symptom without diagnosis) — never invent a plausible-looking cause; if the applied solution was not validated as effective (ticket closed without user or QA confirmation), mark the whole article as a low-confidence draft…
- Next: `16-02-diagnostico-respuesta-incidente-soporte`

### 16.4 — Severity-Based Escalation and SLA Matrix
- File: [references/16-04-matriz-escalamiento-sla.md](references/16-04-matriz-escalamiento-sla.md)
- When to use it: when first establishing a product/team's support policy, or when reviewing it periodically (change in team capacity, new contractual SLAs, recent incidents that exposed gaps in the escalation chain).
- Inputs: catalog of known incident/ticket types (if available), the support team's real capacity (headcount, coverage hours, existence of on-call), existing contractual SLAs with clients (if any), severity definitions currently in use (even if informal), available esc…
- Permitted autonomy: A0 — Analyze (survey existing SLAs and capacity); A1 — Propose (the severity matrix, SLAs, and escalation chain); never A2/A3 — the matrix requires explicit human approval before being adopted as official support policy
- Stop if: stop and escalate to a human if no real support team capacity data is available (headcount, coverage hours) — never fabricate an SLA matrix without verifying the team can sustain it; flag the proposal as low-confidence if contractual SLAs with clients exist but could not be confirmed
- Next: `16-01-triage-tickets-soporte`

### 16.5 — Aggregate Trend and Root Cause Analysis of Tickets
- File: [references/16-05-analisis-tendencias-tickets.md](references/16-05-analisis-tendencias-tickets.md)
- When to use it: periodically (monthly or quarterly) over a batch of tickets that were already individually handled and closed via `16-02`, as a retrospective exercise that feeds product and engineering decisions.
- Inputs: export or read access to the batch of resolved tickets for the period to analyze (ideally with category, summary, resolution, and resolution time for each), the date range or period to cover, existing category taxonomy if the team already uses one
- Permitted autonomy: A0 — Analyze (reading and aggregate categorization of the batch); A1 — Propose (recommend engineering or documentation initiatives); never A2/A3 — this prompt does not create issues, deploy documentation, or execute product changes
- Stop if: stop and escalate if the available ticket batch is too small or lacks the minimum fields (category, summary, resolution) to support an aggregate pattern — never invent categories or root causes without evidence from at least several repeated tickets; flag as low-confidence any pattern based on fewe…
- Next: `02-04-triage-backlog-github` (skill `sdlc-analysis`), `10-01-documentacion-tecnica` (skill `sdlc-documentation`), `16-06-auditoria-base-conocimiento`

### 16.6 — Support knowledge base health audit
- File: [references/16-06-auditoria-base-conocimiento.md](references/16-06-auditoria-base-conocimiento.md)
- When to use it: periodically (e.g. quarterly) as KB maintenance, or when the support team reports that existing articles no longer reflect the current product or that finding the right answer is difficult.
- Inputs: KB article inventory (title, last-updated date, category, usage/view metrics if any), current product version or recent changelog, recurring ticket categories (from `16-05` if available, or the ticket history directly)
- Permitted autonomy: A0 — Analyze (staleness, duplicates, coverage, usage); A1 — Propose (what to update, merge, archive, or create); never A2/A3 — actually publishing or deleting articles requires human review and execution by the KB owner
- Stop if: stop and flag if no last-updated date is available to evaluate staleness — do not assume an article is current just because there is no evidence it is outdated; if no usage/view metrics exist, limit the "unused" analysis to what can be inferred another way and state it as a proxy, not real usage da…
- Next: `16-03-articulo-base-conocimiento`, `16-05-analisis-tendencias-tickets`

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

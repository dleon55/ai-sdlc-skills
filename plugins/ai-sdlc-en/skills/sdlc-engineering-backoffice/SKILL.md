---
name: sdlc-engineering-backoffice
description: "AI-SDLC prompts for Engineering back office. Use it for engineering team management: technical onboarding and offboarding, tool and license evaluation, team capacity, vendor renewals, stakeholder status reports, post-launch review or sprint retrospective."
license: CC-BY-4.0
---

# AI-SDLC phase 17 — Engineering back office

This skill groups the prompts of the **Engineering back office** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 17.1 — Technical Onboarding Checklist
- File: [references/17-01-onboarding-tecnico.md](references/17-01-onboarding-tecnico.md)
- When to use it: when bringing a new member onto the engineering team, before or during their first day.
- Inputs: role and seniority of the new team member, team tech stack and tooling (repos, cloud provider, CI/CD tooling, secrets manager), access level required by the role, start date, assigned mentor/buddy if any, available internal documentation (wiki, runbooks, arch…
- Permitted autonomy: A0 — Analyze (survey the role, stack, and the team's existing access setup); A1 — Propose (the checklist of access, tools, and documentation to review); never A2/A3 — this prompt does not create accounts, grant permissions, or make changes to identity/access systems
- Stop if: stop and ask for clarification if the role or the team's stack is not specified — never fabricate a generic checklist without context; escalate to whoever holds IAM permissions before any listed access is granted; if information about the team's secrets manager or least-privilege policy is missing,…
- Next: `17-02-offboarding-tecnico`

### 17.2 — Technical Offboarding Checklist
- File: [references/17-02-offboarding-tecnico.md](references/17-02-offboarding-tecnico.md)
- When to use it: as soon as a team member's departure date is confirmed (resignation, termination, contract end, team change resulting in loss of access), ideally with enough lead time to plan knowledge transfer before the last day.
- Inputs: role of the person leaving the team and the access/systems known to be theirs, services/repositories/on-call rotations they own or maintain, confirmed departure date, list of the organization's access-managing systems (repos, cloud, secrets manager, SSO, CI/C…
- Permitted autonomy: A1 — Propose (generates the revocation, transfer, and verification checklist); never A2/A3 — actual access revocation requires human execution with administrative permissions on each system (IAM, SSO, secrets manager, CI/CD), and must be completed on or before the departure date
- Stop if: stop and escalate if the complete list of access or systems the person had access to is not known — explicitly flag it as a residual risk instead of assuming the list is complete; stop if there is no confirmed departure date and use that gap as a blocker to set concrete deadlines in the checklist
- Next: `17-01-onboarding-tecnico`

### 17.3 — Tool/License Adoption Evaluation and Decision
- File: [references/17-03-evaluacion-herramienta-licencia.md](references/17-03-evaluacion-herramienta-licencia.md)
- When to use it: before formally adopting a new tool, SaaS, or paid library that implies recurring cost or dependency on an external vendor.
- Inputs: name of the candidate tool/service, problem or need it solves, known alternatives (or a statement that none have been identified yet), available budget if applicable, proposed licensing model, type of data the tool will touch
- Permitted autonomy: A1 — Propose (evaluation sheet with an adopt/reject/evaluate-further recommendation); never A2/A3 — this prompt does not approve budget or contract the vendor
- Stop if: stop and escalate if no verifiable license price is available — never fabricate plausible-looking figures; stop if no alternative (including the option of not adopting) has been identified for comparison
- Next: `11-08-finops-cloud-cost-audit` (skill `sdlc-operations`)

### 17.4 — Engineering Team Capacity and Workload Report
- File: [references/17-04-reporte-capacidad-equipo.md](references/17-04-reporte-capacidad-equipo.md)
- When to use it: when planning a sprint, quarter, or release with date commitments, or when there are signals of team overload (recurring delays, burnout, critical dependency on a single person).
- Inputs: current team composition (roles, seniority, specialties, weekly availability %), planned absences per person and period (vacation, leave, training), committed backlog or roadmap with effort estimates per item, period to evaluate
- Permitted autonomy: A0 — Analyze (reading team composition, absences, and committed backlog); A1 — Propose (redistribution, replanning, or hiring recommendations); never A2/A3 — this prompt does not reassign tasks or execute personnel decisions, that is delegated to the human lead or manager responsible
- Stop if: stop and escalate if there is no committed backlog/roadmap with effort estimates — never invent plausible-looking estimates; stop if team composition or planned absences are not confirmed and flag it as a residual risk instead of assuming full availability
- Next: `11-10-capacity-planning` (skill `sdlc-operations`), `05-01-plan-implementacion` (skill `sdlc-planning`)

### 17.5 — Vendor and Technology Contract Renewal Audit
- File: [references/17-05-auditoria-renovacion-vendors.md](references/17-05-auditoria-renovacion-vendors.md)
- When to use it: in the cycle leading up to the renewal date of any technology vendor, SaaS, or license contract (ideally with enough lead time to leave room for negotiation or migration before expiration).
- Inputs: current contract or license terms (cost, contracted volume/seats, renewal date, cancellation or penalty clauses), real usage data (active seats, consumed volume, usage frequency by team/feature), known or to-be-researched market alternatives, vendor support o…
- Permitted autonomy: A0 — Analyze (real usage vs. contracted, comparison of alternatives); A1 — Propose (recommendation to renew/renegotiate/migrate/cancel); never A2/A3 — this prompt does not renew, cancel, sign, or negotiate contracts, nor execute migration to an alternative
- Stop if: stop and escalate if no real usage data is available to calculate the usage-vs-contracted ratio — never fabricate plausible-looking utilization figures; flag as a low-confidence recommendation if the comparison with market alternatives relies on outdated or unverified information; escalate as urgen…
- Next: `17-03-evaluacion-herramienta-licencia`

### 17.6 — Stakeholder status report
- File: [references/17-06-reporte-estado-stakeholders.md](references/17-06-reporte-estado-stakeholders.md)
- When to use it: at the close of a sprint or milestone, or on the periodic communication cadence agreed with stakeholders (weekly/biweekly).
- Inputs: committed milestones (from `00-D-01` or the current roadmap), issues/PRs closed and opened in the period, CI/CD status for the period, active risks (from `05-02` or the current register), period to report, audience (expected technical detail level)
- Permitted autonomy: A0 — Analyze (gather real progress from the sources); A1 — Propose (draft the report in business language); never A2/A3 — this prompt does not communicate directly with stakeholders, it produces the document for a human to review and send
- Stop if: stop and explicitly flag if a milestone reported as "in progress" has no verifiable associated issue/PR — do not report progress that cannot be traced to a real source; stop if the period to report is not defined
- Next: `05-02-riesgos-implementacion` (skill `sdlc-planning`), `17-04-reporte-capacidad-equipo`

### 17.7 — Post-launch success review: benefits realization against the Project Charter
- File: [references/17-07-revision-exito-post-lanzamiento.md](references/17-07-revision-exito-post-lanzamiento.md)
- When to use it: weeks or months after launch, once real usage or business data is available — as a project's formal closure step or as a periodic review of already-launched initiatives.
- Inputs: original Project Charter with declared objectives/KPIs (`00-D-01`), real usage/adoption/business data since launch, elapsed time window
- Permitted autonomy: A0 — Analyze
- Stop if: if a Charter KPI cannot be measured with available data, do not invent an approximate value — report it as "not measurable" and flag what instrumentation would be needed to measure it next time
- Next: `11-03-deuda-tecnica` (skill `sdlc-operations`)

### 17.8 — Team retrospective per sprint/iteration
- File: [references/17-08-retrospectiva-equipo-sprint.md](references/17-08-retrospectiva-equipo-sprint.md)
- When to use it: at the close of each sprint or iteration, as a structured input to (or written record of) the team's retrospective meeting.
- Inputs: what happened in the current sprint/iteration (as reported by the team, not inferred), previous retrospective(s) with their pending improvement actions, if any
- Permitted autonomy: A0 — Analyze; A1 — Propose (prioritized improvement actions)
- Stop if: do not invent problems, wins, or root causes the team did not explicitly report — if something wasn't mentioned by the team, it isn't included as if it had been; if a previous retrospective's improvement action was never completed, report it explicitly instead of omitting it
- Next: `11-03-deuda-tecnica` (skill `sdlc-operations`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

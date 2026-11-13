---
name: sdlc-operations
description: "AI-SDLC prompts for Operations and SRE. Use it for operating production systems: troubleshooting, hardening, technical debt, incident response, production performance, patching, postmortems and runbooks, rollback, cloud cost (FinOps), capacity, legacy decommissioning, alert noise, on-call health, migration or cutover, and disaster recovery."
license: CC-BY-4.0
---

# AI-SDLC phase 11 — Operations and SRE

This skill groups the prompts of the **Operations and SRE** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 11.1 — Environment troubleshooting
- File: [references/11-01-troubleshooting.md](references/11-01-troubleshooting.md)
- When to use it: when a service fails, a deployment doesn't work as expected, or there's a configuration problem in any environment. If the environment is PROD and there is significant user impact, use `11-04-incident-response` instead.
- Inputs: symptom, environment (DEV/QA/STAGING/PROD), involved services, available evidence (logs, errors, captures)
- Permitted autonomy: A0 — Analyze: diagnosis and hypotheses; the resolution path is left proposed and pending approval before moving to A2
- Stop if: if the environment is PROD and there is significant user impact, it must stop and escalate to `11-04-incident-response` instead of continuing standard troubleshooting
- Next: `11-04-incident-response`, `03-02-causa-raiz` (skill `sdlc-incidents`)

### 11.2 — Security hardening and operations
- File: [references/11-02-hardening-seguridad.md](references/11-02-hardening-seguridad.md)
- When to use it: periodically as security review, before a production deployment, or when security findings are detected in code review.
- Inputs: docker-compose, nginx configuration, `.env` (structure, not values), workflows, GitHub permissions, read access to recent commit history (git log)
- Permitted autonomy: A0 — Analyze (only delivers findings and mitigation plan, does not apply changes)
- Stop if: never include real secret values in the output, even if found exposed; reference only location and type
- Next: `13-08-gestion-secretos-credenciales` (skill `sdlc-security`), `13-03-secure-sdlc-revision` (skill `sdlc-security`)

### 11.3 — Technical debt and continuous improvement
- File: [references/11-03-deuda-tecnica.md](references/11-03-deuda-tecnica.md)
- When to use it: at the close of a sprint, in periodic technical reviews, or when planning structural project improvements.
- Inputs: main branch, components or modules to analyze, access to source code, tests, CI/CD configuration, architecture and documentation
- Permitted autonomy: A0 — Analyze: inventory and recommendations, without applying changes
- Stop if: if it cannot access an area declared as "to analyze" (nonexistent module or outside the repo), it must flag the omission instead of completing the matrix with assumptions
- Next: `05-01-plan-implementacion` (skill `sdlc-planning`), `11-06-gestion-parches-actualizaciones`

### 11.4 — Production incident response runbook
- File: [references/11-04-incident-response.md](references/11-04-incident-response.md)
- When to use it: when an active incident is detected in production, to document the response process afterwards, or to design the project's standard runbook before the first incident occurs.
- Inputs: symptom/alert, affected system, environment, detection time, detection source, stack
- Permitted autonomy: A0 — Analyze in phases 1-3 and 6-7; A3 — Publish in phase 4 (rollback, mitigation, or mutation against live production is a deployment/remote mutation per `00-framework.md`, not execution in an isolated workspace), only if the runbook already authorized the specific action and with the explicit or pre-authorized-policy approval that A3 requires
- Stop if: the prompt itself requires stopping all AI agent operations in the repository and not deploying code while the incident is active
- Next: `03-02-causa-raiz` (skill `sdlc-incidents`), `11-07-sre-postmortem-runbook`

### 11.5 — Production Performance: Diagnosis and Optimization
- File: [references/11-05-performance-produccion-diagnostico.md](references/11-05-performance-produccion-diagnostico.md)
- When to use it: Prompt to diagnose, analyze, and remediate performance problems in production: identifies bottlenecks in the application, database, and infrastructure using real observability signals, profiles the system under real load, and delivers an optimization plan with quantifiable changes.
- Inputs: metrics/traces/logs from the degradation period (from `10-04` or Grafana/Datadog/CloudWatch export), technology stack, infrastructure, impacted SLO; optionally thresholds from `07-06`/`07-11`
- Permitted autonomy: A0 — Analyze in characterization, trace/log analysis, and layer-by-layer diagnosis; A1 — Propose in the optimization plan; A2 — Execute controlled only for profiling on staging or to apply already-approved optimizations
- Stop if: if the required profiling can only run in production and no staging with mirrored traffic is available, it must stop and request explicit approval before profiling live
- Next: `07-06-pruebas-performance-carga` (skill `sdlc-testing`), `10-04-observabilidad-instrumentacion` (skill `sdlc-documentation`)

### 11.6 — Patch and Update Management
- File: [references/11-06-gestion-parches-actualizaciones.md](references/11-06-gestion-parches-actualizaciones.md)
- When to use it: Prompt to plan and execute the complete patch management cycle: dependency and component inventory, update criticality assessment, environment-by-environment application plan, regression verification, and cycle documentation. Covers application dependencies, operating system, containers, and infrastructure.
- Inputs: technology stack, available environments, vulnerability context (result from `13-02` SCA if available), CI/CD tools, existing automation, last patch date, committed security SLAs
- Permitted autonomy: A0 — Analyze in inventory and classification; A1 — Propose in the grouped application plan; A2 — Execute controlled in dev/staging; A3 — Publish only for the production deployment, and only with explicit approval from the rollback owner
- Stop if: if a MAJOR update with breaking changes has not remained stable on staging for at least 24h, if the rollback criterion (error rate/P95) is not defined before deploying to production, or if explicit, documented approval from the rollback owner has not been obtained before executing the production de…
- Next: `13-02-sca-analisis-dependencias` (skill `sdlc-security`), `11-07-sre-postmortem-runbook`

### 11.7 — Blameless Post-Mortem and Runbook Generation (SRE)
- File: [references/11-07-sre-postmortem-runbook.md](references/11-07-sre-postmortem-runbook.md)
- When to use it: Immediately after resolving a critical incident or production outage (Phase 03 completed), to document institutional learning.
- Inputs: raw incident data (timeline, logs, chat), applied resolution; optionally the root cause analysis result from `03-02`
- Permitted autonomy: A1 — Propose: delivers the post-mortem document and the proposed runbook; adopting it as the official runbook operable by on-call requires human review (A3)
- Stop if: if the 5 Whys analysis converges on attributing the failure to a person instead of a system or process, it must reframe the finding in blameless terms before continuing; if there is insufficient incident data, it must flag that instead of inventing the timeline
- Next: `10-04-observabilidad-instrumentacion` (skill `sdlc-documentation`), `11-06-gestion-parches-actualizaciones`

### 11.8 — FinOps Audit and Cloud Cost Efficiency
- File: [references/11-08-finops-cloud-cost-audit.md](references/11-08-finops-cloud-cost-audit.md)
- When to use it: Before provisioning new infrastructure, during periodic billing reviews, or when evaluating architectures for cloud migrations.
- Inputs: infrastructure code (Terraform, CDK, Kubernetes manifests) or architecture description, cloud provider
- Permitted autonomy: A1 — Propose
- Stop if: do not recommend Spot Instances or storage-tier changes for interruption-intolerant workloads without explicitly flagging that risk
- Next: `09-03-workflows-github-actions` (skill `sdlc-integration`)

### 11.9 — Rollback Execution Runbook
- File: [references/11-09-runbook-rollback.md](references/11-09-runbook-rollback.md)
- When to use it: when a recently shipped change is causing problems and a rollback is being considered or executed.
- Inputs: symptom driving the rollback, affected component(s) and their change type (code / DB migration / config or feature flag / infrastructure), target version or state to revert to, whether data was written on the new version, environment
- Permitted autonomy: A1 — Propose for the entire design of the decision criteria and the rollback runbook; A2 — Execute controlled only in an isolated environment (staging/QA) once the explicit preconditions are already verified (previous version confirmed deployable, migration reversibility confirmed); A3 — Publish to execute the rollback against production, and in particular any rollback touching a database migration or production data — this is a deployment/remote mutation per `00-framework.md`, not execution in an isolated workspace, and requires the explicit or pre-authorized-policy approval that A3 requires before each action — this prompt does not grant itself broader execution rights than that
- Stop if: stop and escalate if a database migration's reversibility cannot be confirmed; stop if it cannot be confirmed that the previous version is deployable (dependencies, configuration); stop if the rollback would imply data loss not explicitly accepted by the system's responsible party; do not execute a…
- Next: `11-07-sre-postmortem-runbook`

### 11.10 — Capacity Planning and Scaling Forecast
- File: [references/11-10-capacity-planning.md](references/11-10-capacity-planning.md)
- When to use it: when planning for expected growth (traffic, data volume, user base) before it happens, or after `07-06-pruebas-performance-carga` reveals a capacity ceiling under current load that needs a forward-looking capacity plan.
- Inputs: current utilization metrics per layer (compute, DB connections/storage, cache, third-party API rate limits, queue depth), expected growth hypothesis and its source (real business projection or assumption), load-test results if available (`07-06`)
- Permitted autonomy: A0 — Analyze (metrics reading and projection); A1 — Propose (scaling plan and thresholds); never A2/A3 — this prompt does not provision, resize, or modify infrastructure
- Stop if: stop and escalate if no real utilization metric is available for the critical component — never fabricate plausible-looking figures; flag the projection as low-confidence if the growth hypothesis is an unsupported assumption
- Next: `07-06-pruebas-performance-carga` (skill `sdlc-testing`), `11-08-finops-cloud-cost-audit`

### 11.11 — Legacy system/service decommission plan
- File: [references/11-11-plan-decomiso-sistema-legacy.md](references/11-11-plan-decomiso-sistema-legacy.md)
- When to use it: when a decision is made to fully retire a system, service, or database, before executing any shutdown action.
- Inputs: system/service to decommission, known inventory of consumers/integrations, applicable data retention obligations, target shutdown date, availability of recent access/traffic logs for the system
- Permitted autonomy: A0 — Analyze (dependent inventory, retention obligations); A1 — Propose (communication plan and shutdown sequence); A3 — Publish only to execute each shutdown phase (disable writes, switch to read-only, final shutdown) against the real system, and only with explicit approval before each phase — it does not execute any shutdown phase on its own
- Stop if: stop if recent access/traffic logs are unavailable or do not cover a representative period — do not assume "no visible traffic" means "no dependents"; stop if a data retention obligation exists without a compliance plan before the shutdown date
- Next: `04-05-versionado-deprecacion-api` (skill `sdlc-design`), `11-09-runbook-rollback`

### 11.12 — Alert noise audit (alert fatigue)
- File: [references/11-12-auditoria-ruido-alertas.md](references/11-12-auditoria-ruido-alertas.md)
- When to use it: when the team reports alert fatigue (too many notifications, alerts habitually ignored), or periodically as a health check of an already-in-production monitoring system.
- Inputs: history of alerts fired in the period (name, timestamp, severity, whether action was taken, whether silenced), access to current dashboards/alert rules, definition of what constitutes "action taken", if any
- Permitted autonomy: A0 — Analyze (classify alerts as noise/signal); A1 — Propose (tuning, consolidation, or removal recommendation); never A2/A3 — actually modifying alert rules requires a human to apply it after reviewing the recommendation
- Stop if: stop and flag if the alert history does not record whether action was taken — do not assume "no visible action" is equivalent to "confirmed noise" without verifying with the team; if the analyzed period is too short for low-frequency alerts, flag the limitation instead of concluding it is noise
- Next: `10-04-observabilidad-instrumentacion` (skill `sdlc-documentation`), `11-13-salud-rotacion-oncall`

### 11.13 — On-call rotation health audit
- File: [references/11-13-salud-rotacion-oncall.md](references/11-13-salud-rotacion-oncall.md)
- When to use it: periodically as a health check of the on-call schedule, or when the team reports fatigue, complaints of rotation inequity, or signals of high staff turnover in on-call roles.
- Inputs: period's page/alert history (who received it, timestamp, time band), configured rotation schedule (who is on call when), period to evaluate, qualitative burnout or complaint signals if any (optional)
- Permitted autonomy: A0 — Analyze (real page distribution, rotation fairness); A1 — Propose (rebalancing recommendation); never A2/A3 — actually changing the on-call schedule requires human decision and execution by the responsible lead or manager
- Stop if: stop if the page history does not distinguish business hours from night/weekend — do not assume all pages carry the same fatigue cost; stop if the configured rotation schedule is not available, do not infer shifts from the page history alone
- Next: `17-04-reporte-capacidad-equipo` (skill `sdlc-engineering-backoffice`), `11-12-auditoria-ruido-alertas`

### 11.14 — Platform or legacy system migration and cutover plan
- File: [references/11-14-migracion-cutover-plataforma.md](references/11-14-migracion-cutover-plataforma.md)
- When to use it: when deciding to move an application, its data, or its traffic from an old system/stack/cloud to a new one (major stack upgrade, cloud migration, system consolidation, monolith→microservices) — before executing any real cutover, and as a mandatory prior step to `11-11` if the end goal is to shut down the source system.
- Inputs: source and target systems (description, stack, data volume), target architecture if it exists (`00-D-02`/`04-01`), tolerable downtime constraints, known dependents of the source system (`11-11` inventory if it exists)
- Permitted autonomy: A1 — Propose
- Stop if: if a data-consistency verification strategy between source and target cannot be confirmed, do not declare the cutover plan ready to execute — mark it blocking instead of assuming consistency
- Next: `11-11-plan-decomiso-sistema-legacy`, `11-09-runbook-rollback`

### 11.15 — Disaster recovery and business continuity plan (DR/BCP)
- File: [references/11-15-plan-recuperacion-desastres-continuidad.md](references/11-15-plan-recuperacion-desastres-continuidad.md)
- When to use it: when defining the initial architecture of a critical system (after `00-D-02`, where RPO/RTO objectives are declared), periodically to validate that the real recovery capability still meets those objectives, or when preparing the first formal recovery test (drill) of a system that has never been tested.
- Inputs: declared RTO/RPO objectives (`00-D-02` or another source), system architecture and its critical dependencies, current backup mechanism (if any), last restore test performed (if any)
- Permitted autonomy: A1 — Propose
- Stop if: if it cannot be confirmed that the target RTO/RPO is achievable with the current backup/replication mechanism, do not declare the system "recoverable" — flag it as a capability gap and report the real estimated RTO/RPO instead
- Next: `11-07-sre-postmortem-runbook`, `00-D-04-registro-riesgos-proyecto` (skill `sdlc-foundations`)

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

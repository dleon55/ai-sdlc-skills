---
name: sdlc-testing
description: "AI-SDLC prompts for Testing. Use it when asked to design or implement tests: unit, integration, E2E, smoke, performance and load, accessibility, flaky test diagnosis, test data, test stack detection or a master test plan."
license: CC-BY-4.0
---

# AI-SDLC phase 07 — Testing

This skill groups the prompts of the **Testing** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 7.0 — Test Stack Detection
- File: [references/07-00-deteccion-stack-pruebas.md](references/07-00-deteccion-stack-pruebas.md)
- When to use it: Prompt to detect and document the active test stack in the repository. Produces a structured **test stack profile** that is attached as context to implementation prompts (`07-07` through `07-11`), eliminating the need for each agent to re-discover the project's tools and conventions.
- Inputs: read access to the repository: root configuration files (package.json, pyproject.toml, pom.xml, etc.), CI/CD workflows, existing tests directory
- Permitted autonomy: A0 — Analyze (reading and inventory); applies no changes and requires no approval
- Stop if: explicitly mark a field "not detected" instead of assuming or inventing a framework, command, or convention not backed by a real file in the repository
- Next: `07-01-pruebas-unitarias`, `07-07-implementacion-pruebas-unitarias`, `07-15-plan-maestro-pruebas`

### 7.1 — Unit test design
- File: [references/07-01-pruebas-unitarias.md](references/07-01-pruebas-unitarias.md)
- When to use it: after implementing changes, in parallel with implementation, or as reference before writing code.
- Inputs: implemented code or proposed changes, acceptance criteria, test stack profile (`07-00`) if available
- Permitted autonomy: A1 — Propose (test matrix as an artifact, without implementing the test code)
- Stop if: stop if there is no reference code or acceptance criteria; explicitly flag if the recommended coverage cannot be achieved with the available information instead of inventing scenarios
- Next: `07-07-implementacion-pruebas-unitarias`

### 7.2 — Integration test design
- File: [references/07-02-pruebas-integracion.md](references/07-02-pruebas-integracion.md)
- When to use it: after unit tests (`07-01`), to validate that modules work correctly together.
- Inputs: API contracts, integration design, available test data, unit test matrix (`07-01`) if it exists
- Permitted autonomy: A1 — Propose (integration test plan without implementing it)
- Stop if: stop if there are no reference API contracts or integration design; never use real production data as test data, only synthetic or anonymized data
- Next: `07-08-implementacion-pruebas-integracion`

### 7.3 — E2E test design
- File: [references/07-03-pruebas-e2e.md](references/07-03-pruebas-e2e.md)
- When to use it: after integration tests (`07-02`), to validate the complete flow from the user perspective.
- Inputs: use case or requirement to cover, acceptance criteria, reference to the prior integration plan (`07-02`)
- Permitted autonomy: A1 — Propose (delivers a plan/artifact without applying it; execution happens in `07-09`)
- Stop if: stop and request clarification if the use case or acceptance criteria are not defined in enough detail to derive steps, expected result, and evidence
- Next: `07-09-implementacion-pruebas-e2e`

### 7.4 — Smoke tests
- File: [references/07-04-pruebas-humo.md](references/07-04-pruebas-humo.md)
- When to use it: immediately after a deployment or merge, for a quick health validation before complete tests.
- Inputs: documented critical flows, reference to the deployed branch or version, target environment (QA/STAGING/PROD)
- Permitted autonomy: A1 — Propose (delivers a prioritized checklist as an artifact, without executing it against the system)
- Stop if: stop if no critical flows are identified or the target environment is undefined, since the checklist would lose its usefulness as a quick validation
- Next: `07-10-implementacion-pruebas-humo`

### 7.5 — Browser automation with Google Antigravity
- File: [references/07-05-automatizacion-antigravity.md](references/07-05-automatizacion-antigravity.md)
- When to use it: to automate E2E or regression tests of critical flows impacted by the change. Use this prompt instead of `07-03`+`07-09` when the automation will run through Google Antigravity's browser agent (autonomous verification with captures/video) rather than a traditional E2E scripting framework.
- Inputs: use cases or critical flows to automate, prior E2E plan if it exists, UI design, base URL of the QA/STAGING environment
- Permitted autonomy: A1 — Propose (delivers the strategy as an artifact; autonomous execution by Google Antigravity is a later external step that requires the environment and test credentials to already be authorized)
- Stop if: stop if the target environment is not QA/STAGING (never automate directly against production); stop if stable selectors or test data are missing, since that would produce fragile automation

### 7.6 — Performance and load tests
- File: [references/07-06-pruebas-performance-carga.md](references/07-06-pruebas-performance-carga.md)
- When to use it: before deploying to production changes that affect APIs, database queries, batch processes, file generation or any component with performance requirements. Also as periodic system health review.
- Inputs: components to test, test environment (QA/Staging — never production), expected concurrent users in production, acceptable SLA or response time, available tool (k6/Locust/JMeter/Artillery/hey/wrk)
- Permitted autonomy: A1 — Propose (strategy, scenarios, and base script) — this prompt never executes load tests under any autonomy level; execution (even in QA/Staging with approval) is the exclusive responsibility of `07-11-implementacion-pruebas-performance`
- Stop if: stop and escalate if the proposed environment is production; do not run the test if no SLA or failure thresholds are defined; never use real user or production data in test payloads
- Next: `07-11-implementacion-pruebas-performance`

### 7.7 — Unit Test Implementation
- File: [references/07-07-implementacion-pruebas-unitarias.md](references/07-07-implementacion-pruebas-unitarias.md)
- When to use it: Prompt to generate executable unit test code from the design defined in `07-01`. Produces test files ready to run in the project's test framework.
- Inputs: Test stack profile (`07-00`) and unit test design matrix (`07-01`) attached or referenced; access to the source code of the units under test
- Permitted autonomy: A2 — Execute controlled (writes and runs test files in the workspace, without publishing changes)
- Stop if: never modify source code; stop after a maximum of 3 self-correction cycles if compilation or assertion failures persist, and report the exact diagnostics instead of continuing to retry
- Next: `07-08-implementacion-pruebas-integracion`

### 7.8 — Integration Test Implementation
- File: [references/07-08-implementacion-pruebas-integracion.md](references/07-08-implementacion-pruebas-integracion.md)
- When to use it: Prompt to generate executable integration test code from the design defined in `07-02`. Validates real interaction between modules, services, APIs, and the database using the project's test framework.
- Inputs: Test stack profile (`07-00`) and integration test plan (`07-02`) attached or referenced; available or simulable test environment (containers, stubs)
- Permitted autonomy: A2 — Execute controlled (writes, runs, and tears down state in the workspace or an isolated test environment)
- Stop if: stop if a required external dependency cannot be simulated with a stub or container and the test would depend on a real production service; stop if teardown cannot guarantee state isolation between runs
- Next: `07-09-implementacion-pruebas-e2e`

### 7.9 — E2E Test Implementation
- File: [references/07-09-implementacion-pruebas-e2e.md](references/07-09-implementacion-pruebas-e2e.md)
- When to use it: Prompt to generate executable end-to-end test code from the design defined in `07-03`. Produces automation scripts that validate complete flows from the user interface to the final result, using the project's E2E framework.
- Inputs: Test stack profile (`07-00`) and E2E test plan (`07-03`) attached or referenced; application deployed and accessible in a test environment (QA/staging) with test credentials
- Permitted autonomy: A2 — Execute controlled (runs scripts against an isolated test environment, never against production)
- Stop if: stop if the target URL points to production; stop if the flow would require real user data; stop and document if cleanup of the generated state (created records) cannot be guaranteed at the end of the test
- Next: `07-04-pruebas-humo`, `07-10-implementacion-pruebas-humo`

### 7.10 — Smoke Test Implementation
- File: [references/07-10-implementacion-pruebas-humo.md](references/07-10-implementacion-pruebas-humo.md)
- When to use it: Prompt to generate an executable smoke test script from the checklist defined in `07-04`. Produces an automatable artifact that validates in minutes that the system is operational after a deployment.
- Inputs: smoke test checklist generated by `07-04`, Test stack profile from `07-00`, documented health endpoints or critical flows
- Permitted autonomy: A2 — Execute controlled
- Stop if: if the `07-04` checklist does not exist or is incomplete, or if any check would require writing or modifying business data to verify itself, stop and escalate instead of improvising the check
- Next: `09-04-promotion-checklist` (skill `sdlc-integration`)

### 7.11 — Performance and Load Test Implementation
- File: [references/07-11-implementacion-pruebas-performance.md](references/07-11-implementacion-pruebas-performance.md)
- When to use it: Prompt to generate executable performance, load, stress, and benchmark test code from the design defined in `07-06`. Produces scripts ready to run with the project's load testing tool.
- Inputs: performance test design from `07-06` (scenarios, thresholds, selected tool), Test stack profile from `07-00`, test environment URL and authentication scheme
- Permitted autonomy: A2 — Execute controlled for load/benchmark tests on staging; explicit A3 with an approved maintenance window for any stress/spike/soak run against production
- Stop if: if no staging environment is available, if the base URL points to production without a confirmed maintenance window, or if the provided credentials are not synthetic/test data, stop and escalate
- Next: `11-05-performance-produccion-diagnostico` (skill `sdlc-operations`)

### 7.12 — Accessibility (a11y) Audit and UX Compliance
- File: [references/07-12-accessibility-a11y-audit.md](references/07-12-accessibility-a11y-audit.md)
- When to use it: Before merging a Pull Request that introduces or modifies visual frontend components, or when auditing an existing system to meet accessibility regulations.
- Inputs: source code of the component or view (`frontend_code`) and the UI framework used (`ui_framework`)
- Permitted autonomy: A1 — Propose (delivers report and corrected code as a proposal; does not apply the change directly to the repository)
- Stop if: if the code fragment lacks enough context to evaluate a criterion (e.g., color contrast defined in an external, unprovided stylesheet, or dynamic behavior not visible in the snippet), document it as an evidence limitation instead of assuming compliance or non-compliance
- Next: `08-01-revision-completa-pr` (skill `sdlc-review`)

### 7.13 — Flaky test diagnosis and stabilization
- File: [references/07-13-diagnostico-tests-flaky.md](references/07-13-diagnostico-tests-flaky.md)
- When to use it: when an existing test fails intermittently in CI or locally with no apparent code changes, before deciding whether to ignore it, auto-retry it, or fix it at the root.
- Inputs: test name/path, recent CI run history (pass/fail, timestamps), logs or stack traces from at least 2-3 failures, the test's code and the related code under test, whether it also fails locally or only in CI
- Permitted autonomy: A0 — Analyze (root-cause diagnosis); A1 — Propose (fix, quarantine, or removal); A2 — Execute controlled only to run the test repeatedly in an isolated environment for the purpose of reproducing the pattern, never to apply the fix without human review
- Stop if: if the failure cannot be reproduced after the number of runs defined in the protocol, state "not reproduced" instead of guessing the cause; never recommend permanent quarantine without a follow-up ticket and review date
- Next: `11-03-deuda-tecnica` (skill `sdlc-operations`)

### 7.14 — QA test data management strategy
- File: [references/07-14-gestion-datos-prueba.md](references/07-14-gestion-datos-prueba.md)
- When to use it: when setting up a new shared QA/staging environment, or when test failures appear due to inconsistent/contaminated data between runs or collisions between parallel executions.
- Inputs: test environment(s) to cover, dataset origin (synthetic / masked production snapshot / mixed), data volume needed for representativeness, number of pipelines/agents running in parallel, applicable compliance policy for the data (PII, PCI, or other, if any)
- Permitted autonomy: A1 — Propose (strategy and scripts); A2 — Execute controlled only in the indicated isolated test environment, never against production or a shared environment without explicit approval
- Stop if: stop if asked to start from a production snapshot without an already-defined PII/sensitive-data masking policy — do not design the masking on your own without that policy; stop if the data volume needed for representative tests cannot be confirmed
- Next: `13-08-gestion-secretos-credenciales` (skill `sdlc-security`)

### 7.15 — Master test plan: project QA strategy
- File: [references/07-15-plan-maestro-pruebas.md](references/07-15-plan-maestro-pruebas.md)
- When to use it: at the start of a project (after `07-00`, test-stack detection) or when planning a major release/milestone, before designing individual per-type tests (`07-01` through `07-06`).
- Inputs: test-stack profile (`07-00`) if it exists, project or release scope, relevant non-functional requirements (`02-06`) if they exist, QA time/resource constraints, available environments
- Permitted autonomy: A1 — Propose
- Stop if: if an objective, verifiable exit criterion cannot be defined for at least the critical levels (unit, integration, E2E of the core flows), do not declare the strategy complete — report it as a pending gap instead of filling it with a subjective criterion
- Next: `07-01-pruebas-unitarias`

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

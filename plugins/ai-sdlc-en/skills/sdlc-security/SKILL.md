---
name: sdlc-security
description: "AI-SDLC prompts for Security. Use it for authorized security work: SAST, dependency analysis (SCA), Secure SDLC review, threat modeling, DAST, authorized penetration testing, vulnerability and CVE management, secrets management, or data privacy impact assessment (DPIA)."
license: CC-BY-4.0
---

# AI-SDLC phase 13 — Security

This skill groups the prompts of the **Security** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 13.1 — SAST: Static Application Security Testing
- File: [references/13-01-sast-analisis-seguridad-codigo.md](references/13-01-sast-analisis-seguridad-codigo.md)
- When to use it: Prompt to perform a static security analysis of source code (SAST — Static Application Security Testing): detects OWASP Top 10 vulnerabilities, insecure patterns, improper handling of sensitive data, authentication/authorization issues, and security debt before they reach production.
- Inputs: source code and branch to analyze, language/framework, authentication model in use, type of sensitive data handled; `13-04` (Threat Modeling) result if it exists
- Permitted autonomy: A0 — Analyze
- Stop if: if the language, framework, or data entry points cannot be determined, state this explicitly instead of inventing findings; do not reclassify severity without cited code evidence
- Next: `13-07-gestion-vulnerabilidades-cves`, `08-03-remediacion-maestro` (skill `sdlc-review`)

### 13.2 — SCA: Software Composition Analysis and Dependencies
- File: [references/13-02-sca-analisis-dependencias.md](references/13-02-sca-analisis-dependencias.md)
- When to use it: Prompt to analyze third-party dependencies of the project and identify known vulnerabilities (CVEs), problematic licenses, abandoned dependencies, and supply chain risks. Applies to direct and indirect (transitive) dependencies.
- Inputs: the project's dependency management files and lock files (package.json, requirements.txt, go.mod, etc.), product type (commercial/open source/internal) for license analysis; previous `13-07` findings if they exist
- Permitted autonomy: A0 — Analyze
- Stop if: if lock files are not accessible, state the analysis as incomplete and indicate what is missing instead of simulating nonexistent CVEs; escalate to legal/compliance for problematic or unlicensed dependencies
- Next: `13-07-gestion-vulnerabilidades-cves`

### 13.3 — Secure SDLC Review
- File: [references/13-03-secure-sdlc-revision.md](references/13-03-secure-sdlc-revision.md)
- When to use it: Prompt to verify that required security controls have been applied in each phase of the development cycle: from design to deployment. Acts as a structured Secure SDLC checklist based on OWASP SAMM, NIST SSDF, and Microsoft SDL, adaptable to new projects and incremental changes.
- Inputs: current cycle phase, available results from `13-01` (SAST), `13-02` (SCA), and `13-04` (Threat Modeling), project architecture and CI/CD workflows
- Permitted autonomy: A0 — Analyze the status of each control; A1 — Propose the improvement plan and the prioritized maturity roadmap
- Stop if: mark a control as "⚠️ partial" or "❌ non-compliant" instead of "✅ compliant" if there is no citable verifiable evidence; stop and escalate if a secret in code or a missing critical production control is detected
- Next: `08-03-remediacion-maestro` (skill `sdlc-review`), `05-01-plan-implementacion` (skill `sdlc-planning`), `13-05-dast-analisis-dinamico-seguridad`

### 13.4 — Threat Modeling
- File: [references/13-04-threat-modeling.md](references/13-04-threat-modeling.md)
- When to use it: Prompt to perform threat modeling of a system, component, or feature before or during its design. Identifies attack surfaces, malicious actors, threat vectors, and mitigation controls using the STRIDE methodology. Generates security input for prompts `13-01` (SAST) and `13-03` (Secure SDLC review).
- Inputs: description of the system/component to model, solution design (`04-01`) or use cases (`04-03`) if they exist, architecture or flow diagrams (`04-02`), authentication model and sensitive data involved
- Permitted autonomy: A0 — Analyze the design and generate the STRIDE threat model
- Stop if: do not invent components, flows, or integrations that are not described in the actual design or code; if no design is available, request it before modeling speculative threats
- Next: `13-01-sast-analisis-seguridad-codigo`

### 13.5 — DAST: Dynamic Application Security Analysis
- File: [references/13-05-dast-analisis-dinamico-seguridad.md](references/13-05-dast-analisis-dinamico-seguridad.md)
- When to use it: Prompt to design and execute dynamic application security testing (DAST) against a running application: identifies exploitable vulnerabilities in real time, validates the exposed attack surface, and tests security controls at the transport layer, authentication, session management, and APIs.
- Inputs: isolated test environment (base URL), stack, application type, authentication mechanism; results from `13-04` and `13-01` if available
- Permitted autonomy: A2 — Execute controlled, limited to the isolated environment declared as input
- Stop if: never run against production without explicit, documented authorization; stop if the test environment is not confirmed as isolated
- Next: `13-06-ethical-hacking-pentesting`, `08-03-remediacion-maestro` (skill `sdlc-review`)

### 13.6 — Ethical Hacking and Penetration Testing
- File: [references/13-06-ethical-hacking-pentesting.md](references/13-06-ethical-hacking-pentesting.md)
- When to use it: Prompt to plan and execute structured penetration tests (pentesting) on the application and its infrastructure: defines scope, methodology (OWASP Testing Guide / PTES), reconnaissance phases, controlled exploitation, and documentary evidence. Designed to validate that security controls withstand real attacks.
- Inputs: explicit authorized scope (included/excluded domains, IPs, systems), test environment, box type, prior results from `13-04`/`13-01`/`13-05` if available
- Permitted autonomy: A2 — Execute controlled, only within the scope and time window authorized in writing
- Stop if: requires explicit authorization from the system owner before any exploitation technique; never execute destructive actions, DoS/DDoS, or social engineering against real people
- Next: `08-03-remediacion-maestro` (skill `sdlc-review`)

### 13.7 — Vulnerability Analysis and CVE Management
- File: [references/13-07-gestion-vulnerabilidades-cves.md](references/13-07-gestion-vulnerabilidades-cves.md)
- When to use it: Prompt to perform triage, classification, prioritization, and full lifecycle management of vulnerabilities detected by any security tool (SAST, SCA, DAST, pentesting, scanners). Converts raw findings into an actionable security backlog with remediation SLAs.
- Inputs: reports from the security tools already run (`13-01`, `13-02`, `13-05`, `13-06`, or automated scanners), criticality of the affected system, project-defined remediation SLAs (or use the standard ones)
- Permitted autonomy: A1 — Propose the prioritized security backlog, without creating issues or applying changes directly
- Stop if: do not classify a finding as a false positive or accepted risk without documenting the reasoning and, for "accepted with risk," without explicit approval and a review date; if an actively exploited public exploit exists, escalate the SLA to immediate with no exception
- Next: `08-03-remediacion-maestro` (skill `sdlc-review`)

### 13.8 — Secrets and Credentials Management
- File: [references/13-08-gestion-secretos-credenciales.md](references/13-08-gestion-secretos-credenciales.md)
- When to use it: Prompt to audit, classify, and remediate secrets management in source code, infrastructure, CI/CD pipelines, and runtime environments: detects hardcoded credentials, exposed tokens, insecure configurations, and establishes secure secrets management practices with rotation and centralized storage.
- Inputs: technology stack, current secrets manager, CI/CD used, service providers with credentials, depth of Git history analysis
- Permitted autonomy: A0 — Analyze for inventory and classification; A1 — Propose for the remediation plan; never automatic A2/A3 to revoke/rotate secrets or rewrite history without approval
- Stop if: never include the real value of a detected secret in the output, only its location and type; stop before running `git filter-repo` without explicit team coordination (requires a forced push)
- Next: `13-03-secure-sdlc-revision`

### 13.9 — Data Privacy Impact Assessment (DPIA)
- File: [references/13-09-dpia-privacidad-datos.md](references/13-09-dpia-privacidad-datos.md)
- When to use it: when designing a feature that processes new personal or sensitive data, or before a significant change in how already-existing data is processed.
- Inputs: description of the personal/sensitive data processed, purpose of the processing, proposed legal basis, third parties involved (processors/sub-processors), geographic location of users and of storage
- Permitted autonomy: A0 — Analyze; A1 — Propose (suggested legal basis, mitigation controls)
- Stop if: if a valid legal basis for the processing cannot be determined, do not assume one — report it as blocking, requiring a legal decision before proceeding
- Next: `13-04-threat-modeling`, `13-08-gestion-secretos-credenciales`

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

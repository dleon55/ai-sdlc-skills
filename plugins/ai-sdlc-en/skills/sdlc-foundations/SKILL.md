---
name: sdlc-foundations
description: "AI-SDLC prompts for Project foundations and agent governance. Use it when starting a project or a new repository: project charter, business case, initial stack and architecture, work plan, risk register, repository scaffolding, GitHub configuration, AI agent governance, methodology, code-quality stack, or writing an issue and a plan for an AI agent to execute."
license: CC-BY-4.0
---

# AI-SDLC phase 00 — Project foundations and agent governance

This skill groups the prompts of the **Project foundations and agent governance** phase of the AI-SDLC framework. Each prompt is complete under `references/`.

## How to use it

1. Read `references/00-framework.md` first: it is the mandatory context that precedes every prompt.
2. Pick the prompt below that matches the request and open only that file from `references/`.
3. Ask the user for the bracketed variables (`[MODULE]`, `[PASTE]`, …) you cannot obtain from the repository; do not invent them.
4. Respect the permitted autonomy and stop as soon as a stop criterion is met: state the gap instead of assuming.
5. When done, suggest the recommended next prompt.

## Prompts in this phase

### 0-B.1 — Repository Scaffolding for New Project
- File: [references/00-B-01-scaffolding-repositorio.md](references/00-B-01-scaffolding-repositorio.md)
- When to use it: Prompt to design and generate the base structure of a new repository: directories, configuration files, governance and standards, based on the selected project type, methodology, and technology stack.
- Inputs: project type, methodology, technology stack, hosting/CI platform, team composition, license type
- Permitted autonomy: A1 — Propose
- Stop if: if project type or stack are ambiguous, or an existing structure conflicts with the proposal, state the ambiguity and request confirmation before proposing a full restructuring
- Next: `00-B-03-github-configuracion`, `00-B-05-stack-calidad-codigo`, `00-B-02-gobernanza-ia-agentes`, `00-B-04-metodologia-framework`

### 0-B.2 — AI Agent Governance Configuration Files
- File: [references/00-B-02-gobernanza-ia-agentes.md](references/00-B-02-gobernanza-ia-agentes.md)
- When to use it: Prompt to generate the configuration and governance files that control the behavior of AI agents over the repository: role instructions, coding rules, security restrictions, project context, and work protocol. Compatible with GitHub Copilot, Claude (chat/API and Claude Code), Windsurf, Cursor, Codex, and other agents.
- Inputs: project name and stack, methodology, active AI agent platforms, permitted autonomy level, project critical rules and prohibited patterns, available tools/integrations, data and environment classification
- Permitted autonomy: A1 — Propose
- Stop if: if it cannot be confirmed which agents are actually active in the repository, do not generate configuration for hypothetical agents; if declared critical rules contradict each other, flag the conflict instead of resolving it arbitrarily
- Next: `00-C-03-configuracion-por-agente`

### 0-B.3 — GitHub Repository Configuration (Protections, Templates, and Settings)
- File: [references/00-B-03-github-configuracion.md](references/00-B-03-github-configuracion.md)
- When to use it: Prompt to configure the GitHub repository completely and securely: branch protection, issue and PR templates, Dependabot, GitHub Actions permissions, Environments, secrets, and quality gates. Aligns the platform with the methodology and team maturity level.
- Inputs: GitHub organization/user and repository name, branching methodology, branches to protect, team composition, deployment environments, CI stack
- Permitted autonomy: A1 — Propose
- Stop if: if the current state of branch protection, team roles, or real environments is not known with certainty, state the assumption explicitly instead of generating rules that could block the real team if applied
- Next: `00-B-05-stack-calidad-codigo`

### 0-B.4 — Methodology and Framework Selection and Configuration
- File: [references/00-B-04-metodologia-framework.md](references/00-B-04-metodologia-framework.md)
- When to use it: Prompt to select, document, and operationally configure the project methodology and framework: workflow definition, ceremonies, roles, branching strategy, Definition of Ready, Definition of Done, and how AI agent work integrates into the process.
- Inputs: project type, team size (people + AI agent types), expected delivery frequency, candidate or chosen methodology, third-party integrations/dependencies, current team maturity level
- Permitted autonomy: A1 — Propose
- Stop if: if the candidate methodology requires conditions the declared team does not meet (e.g., full SCRUM with a one-person team), state the alert explicitly instead of recommending it without reservations
- Next: `00-B-01-scaffolding-repositorio`, `00-B-03-github-configuracion`, `17-08-retrospectiva-equipo-sprint` (skill `sdlc-engineering-backoffice`)

### 0-B.5 — Stack and Code Quality Tools Configuration
- File: [references/00-B-05-stack-calidad-codigo.md](references/00-B-05-stack-calidad-codigo.md)
- When to use it: Prompt to select and configure code quality tools according to the project stack: linters, formatters, static analyzers, pre-commit hooks, minimum coverage, and quality gates in CI. Generates ready-to-use configuration files.
- Inputs: main language(s) and framework(s), CI platform, desired minimum coverage, restriction level (permissive/balanced/strict)
- Permitted autonomy: A1 — Propose
- Stop if: if the detected stack is ambiguous or mixed without a clear primary language, request confirmation before generating an exhaustive configuration that might not apply
- Next: `00-B-03-github-configuracion`

### 0-C.1 — Document an Issue Ready for AI Agent Execution
- File: [references/00-C-01-issue-para-agente-ia.md](references/00-C-01-issue-para-agente-ia.md)
- When to use it: Prompt to write a high-quality GitHub issue that can be executed by an AI agent autonomously and in a controlled manner: with sufficient context, verifiable acceptance criteria, explicit restrictions, involved files, and human validation checklist post-execution.
- Inputs: issue title and type, description of the problem/requirement, repository and target branch, environment, involved files/modules (if known), acceptance criteria, restrictions, assigned agent, expected observable result, authorized permissions/tools, budget
- Permitted autonomy: A1 — Propose (drafts the issue and the suggested command; publishing it on GitHub is an A3 action outside this prompt's scope)
- Stop if: if available information does not allow the `## Execution contract` (autonomy mode, tools, scope) to be completed unambiguously, mark the issue "NOT suitable for an agent" in the readiness assessment instead of filling in invented values
- Next: `00-C-02-plan-mode-multiagente`

### 0-C.2 — Safe Plan Mode and Multi-Agent Coordination
- File: [references/00-C-02-plan-mode-multiagente.md](references/00-C-02-plan-mode-multiagente.md)
- When to use it: Prompt to execute any task in **plan mode** before implementing: the agent analyzes, designs, and proposes without touching the code.
- Inputs: reference issue/task, target branch, active parallel agents if known; local repository state (branch, worktrees, recent commits, open PRs)
- Permitted autonomy: A1 — Propose
- Stop if: if Step 2 (conflict detection) finds a potential or active conflict — same file touched by another agent or open PR — STOP immediately and report before continuing; do not move to controlled execution without human confirmation
- Next: `06-01-implementacion-multiagente` (skill `sdlc-implementation`)

### 0-C.3 — Configuration Specific to Each AI Agent Type
- File: [references/00-C-03-configuracion-por-agente.md](references/00-C-03-configuracion-por-agente.md)
- When to use it: Prompt and reference for configuring the behavior, instructions, and restrictions of each AI agent type according to their capabilities and own mechanisms: GitHub Copilot (Agent / Chat / Edits), Claude via chat/API, Claude Code, OpenAI Codex, Windsurf, Cursor, and Google Antigravity.
- Inputs: list of active agents (Copilot, Claude via chat/API, Claude Code, Codex, Windsurf, Cursor, Antigravity), project stack, methodology, project critical rules, general autonomy level; baseline governance already in place (`00-B-02`)
- Permitted autonomy: A1 — Propose
- Stop if: if configuration is requested for an agent without baseline governance in place (`00-B-02`), or if the requested autonomy level for an agent conflicts with the mandatory common rules, flag the conflict before generating the agent-specific configuration
- Next: `00-C-02-plan-mode-multiagente`

### 0-D.1 — Project Charter: Formal Definition of New Project
- File: [references/00-D-01-project-charter.md](references/00-D-01-project-charter.md)
- When to use it: at the start of a new project, when formalizing a project that began without documentation, or when updating scope after a significant strategic change.
- Inputs: project name and type, sponsor, client/end user, business context or need, preliminary technology stack, known constraints, key assumptions
- Permitted autonomy: A1 — Propose (the document requires explicit human signature/approval in section 12 before it is considered in effect)
- Stop if: if critical information for a section (sponsor, scope, budget) is missing and cannot be reasonably inferred from the inputs, mark it with `[PENDING: reason]` instead of inventing figures, dates, or commitments
- Next: `00-D-02-stack-arquitectura-inicial`, `00-B-01-scaffolding-repositorio`

### 0-D.2 — Initial Stack & Architecture: Selection and Documentation of Technical Foundation
- File: [references/00-D-02-stack-arquitectura-inicial.md](references/00-D-02-stack-arquitectura-inicial.md)
- When to use it: after approving the Project Charter (`00-D-01`) and before generating individual ADRs (`04-04-adr-decisiones-arquitectura.md`), repository structure (`00-B-01`), or the implementation plan (`05-01-plan-implementacion.md`).
- Inputs: project name and domain description, system type, known constraints (including compliance), preliminary stack if any, expected scale, deployment platform, team composition; requires the Project Charter (`00-D-01`) to already be approved
- Permitted autonomy: A1 — Propose (decisions marked `[PENDING DECISION]` or `[ADR REQUIRED]` are not considered applied until a formal ADR exists and is subsequently approved)
- Stop if: if a security, compliance, or scalability decision cannot be justified with the available information, mark it `[PENDING DECISION: reason]` and `[ADR REQUIRED]` instead of assuming a definitive choice without evidence
- Next: `04-04-adr-decisiones-arquitectura` (skill `sdlc-design`), `00-B-01-scaffolding-repositorio`

### 0-D.3 — Project work plan: schedule, WBS, and resource allocation
- File: [references/00-D-03-plan-trabajo-proyecto.md](references/00-D-03-plan-trabajo-proyecto.md)
- When to use it: after approving the Project Charter (`00-D-01`) and, if it already exists, the initial stack/architecture (`00-D-02`) — before starting project execution, to have a schedule and resource allocation that the team or sponsor can approve.
- Inputs: approved Project Charter (`00-D-01`), scope and main deliverables, available team (roles, capacity, calendar), deadline or target window if it exists, known external dependencies (other teams, vendors, approvals)
- Permitted autonomy: A1 — Propose (schedule and resource allocation remain marked as a proposal until approved by the sponsor or team)
- Stop if: if the declared deadline is not achievable with the given team and scope, do not adjust the estimates to "make it fit" — report it explicitly as a conflict with the trade-off options; if team capacity information is missing, stop and request it before allocating resources
- Next: `05-02-riesgos-implementacion` (skill `sdlc-planning`), `05-01-plan-implementacion` (skill `sdlc-planning`)

### 0-D.4 — Project risk register (RAID): risks, assumptions, issues and dependencies
- File: [references/00-D-04-registro-riesgos-proyecto.md](references/00-D-04-registro-riesgos-proyecto.md)
- When to use it: together with the Project Charter (`00-D-01`) and the work plan (`00-D-03`), at the start of the project, and reviewed periodically (each milestone or sprint) throughout execution — a risk register filled in only once at the start loses its value.
- Inputs: Project Charter (`00-D-01`), initial stack/architecture (`00-D-02`) if it exists, work plan (`00-D-03`) if it exists, known business constraints, history of materialized risks from similar projects if available
- Permitted autonomy: A0 — Analyze (risks, assumptions, issues, and dependencies already declared or evident in context); A1 — Propose (mitigations, inferred risks not explicitly declared by the business, always marked as a proposal)
- Stop if: if a risk is classified as high (high probability or high impact) with no viable mitigation, do not minimize it or leave it implicit — declare it explicitly as blocking approval of the Charter or the work plan
- Next: `05-02-riesgos-implementacion` (skill `sdlc-planning`)

### 0-D.5 — Feasibility study and business case: should we even do this project?
- File: [references/00-D-05-viabilidad-business-case.md](references/00-D-05-viabilidad-business-case.md)
- When to use it: upon receiving a project idea or business initiative, **before** `00-D-01-project-charter` — this prompt determines whether the project should be formalized at all; the Charter assumes that decision has already been made.
- Inputs: raw idea or initiative, business context, known constraints (maximum budget, deadline, available resources), alternatives already considered if any
- Permitted autonomy: A1 — Propose
- Stop if: if neither cost nor benefit can be estimated with minimal confidence, do not force a go/no-go recommendation — declare "feasibility not determinable with available information" instead of inventing a figure
- Next: `00-D-01-project-charter`

---

Adapted to the SKILL.md format from AI-SDLC Pro — https://prompts.lionsystems.com.mx — CC BY 4.0. Plans: https://prompts.lionsystems.com.mx/precios.html?utm_source=github&utm_medium=skills&utm_campaign=ai-sdlc-skills

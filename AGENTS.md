# Project Guide

## Purpose

This repository defines a request-to-delivery workflow for NestJS-centered fullstack projects: requirements, design, implementation, verification, and reporting. Read [RULES.md](RULES.md) before starting a task; it defines authority, stop conditions, and document rules.

## Current project state

The repository does not yet contain application source code. Stage skills, command procedures, and draft designs for workflow tooling and BA-to-ticket analysis are present; no executable ticket publisher or Python helpers are implemented. See `design/index.md` for design status. Do not describe a planned component as implemented.

| Area | Current state |
| --- | --- |
| Architecture | Not established; record the approved design under `design/docs/system/` when available. |
| Frontend | Not established. |
| Backend | Not established. |
| Database and ORM | Not established. |
| Build and test tools | Not established. |

NestJS is the preferred backend stack for projects using this workflow. The source-backed [NestJS profile](.agents/references/nestjs/project-profile.md) uses `project_education` as a reference for module/DTO/controller/service wiring, Prisma/PostgreSQL and actual local test tooling. It does not establish an application stack in this repository or mandate the reference's package versions. Inspect the target before applying conventions.

## Module map

No application modules exist yet. Add a row when a module exists, and update it when its responsibility or location changes.

| Module | Source path | Responsibility | Main dependencies |
| --- | --- | --- | --- |

## Workflow layout

| Path | Purpose |
| --- | --- |
| `design/index.md` | One row per topic/version, approval status, approver, and decision reference. |
| `design/discovery.md` | Goals, users, MVP, constraints, data, runtime environments, and unknowns. |
| `design/requirements/system/discovery/` | Original project-discovery input. |
| `design/requirements/<topic>/vN/` | Original input supplied for a topic. |
| `design/docs/system/vN/` | Versioned system design. |
| `design/docs/<topic>/vN/` | Versioned analysis and design for a topic. |
| `work/items/<work-id>/` | Work item, pinned versions, plan, impact assessments, and verification evidence across topics. |
| `.agents/commands/` | Procedures for individual steps. |
| `.agents/skills/` | Procedures that coordinate steps into stages. |
| `.agents/references/nestjs/` | Source-backed stack profile, concrete delivery contracts, and verification guidance. |

Command files are Markdown procedures, not executable slash commands. Each command states Input, Gate, Steps, Output, and Done when. Each skill uses YAML `name`/`description`, a short capability summary, linked steps, and an output/gate section. Executable Python helpers will be linked only when implemented.

## Choose a skill

Use the skill named by the user. For a full feature request with no named stage, use `generate-code`. For a request limited to one stage, use the matching stage skill. For one named step, use `run-step`. Read each skill's `SKILL.md` before following it; a skill selects the command files it needs from `.agents/commands/`.

| Task | Skill file |
| --- | --- |
| One command | `.agents/skills/run-step/SKILL.md` |
| Analyze requirements and design | `.agents/skills/analyze-design/SKILL.md` |
| Plan implementation | `.agents/skills/plan-implementation/SKILL.md` |
| Change database schema or migrations | `.agents/skills/implement-database/SKILL.md` |
| Implement backend | `.agents/skills/implement-backend/SKILL.md` |
| Implement frontend | `.agents/skills/implement-frontend/SKILL.md` |
| Test and review | `.agents/skills/verify-and-review/SKILL.md` |
| Run the full workflow | `.agents/skills/generate-code/SKILL.md` |

## Full workflow: `generate-code`

When the skill exists, it coordinates the following stages for a work item that may span multiple topics. Pass each stage's output to the next stage. Run only stages relevant to the task, and obey the gates in `RULES.md`.

Analyze a feature in this order: business goal and rules → user/system flow → feature boundary → data ownership and movement → contracts and affected modules. Describe a simple flow as steps; use a sequence or state diagram when ordering, asynchronous messages, or state transitions matter. Derive implementation architecture from approved system design and current source. For NestJS, run [inspect-nestjs-context](.agents/commands/inspect-nestjs-context.md) and apply [delivery contracts](.agents/references/nestjs/delivery-contracts.md): concrete routes/DTO/access/data decisions, file/symbol tasks, module wiring and checkable acceptance. Reference business rules are not requirements for another project.

Each skill stays within its named stage. At the end, report the work item when present, topics and exact design versions, inputs inspected, work completed, outputs, checks, blockers, and the next permitted stage. The orchestrator persists this handoff in the work item; a standalone skill presents it to the user. A report does not override a design gate.

**Approval gate:** the user or AI may approve a sufficiently supported design using `approve-design-version`. AI records its rationale and may continue in the same run. Planning still requires exact versions marked `approved` in the index. Blocking business questions and explicit requests for user review pause dependent work.

| Stage | Read | Produce or update |
| --- | --- | --- |
| Discover project | User input, existing project documents and source | `design/discovery.md`, preserved input, scope and constraint gaps. |
| Identify work and topics | User request, `RULES.md`, `design/index.md` | Work item, related topics, version references, dependencies and cross-topic acceptance. |
| `analyze-design` | Discovery, original requirements, current system/topic design, relevant source | Versioned design, gap report, and recorded approval when eligible. |
| Assess design change | Current/proposed versions, work item, source and checks | Short impact assessment before adopting a new version; no version change for a code-only correction. |
| `plan-implementation` | Approved design, relevant source and tests | Change plan, acceptance checks, affected files and stages. |
| `implement-database` | Approved data design and change plan | Relevant schema, migrations, and tests. |
| `implement-backend` | Approved API/business design and change plan | Relevant contracts, services, controllers, and tests. |
| `implement-frontend` | Approved UI/flow design and change plan | Relevant API mapping, state, UI, and tests. |
| `verify-and-review` | Acceptance checks including cross-topic flows, changed files, and tests | Local verification evidence, classified findings, and repair routes. |
| Repair and re-verify | Classified findings and the pinned design/plan | Fixes through owning skills, updated evidence, or an explicit blocker. |
| Complete locally | Passing required local checks and resolved blocking findings | Work item `done` and local delivery report. |

Read exact approved versions from the work item; a newer draft does not displace an approved version. The work item links topics without merging their designs. Completion is code changed and checked locally; push, merge, and deployment require separate explicit instructions. If a required skill or command file does not exist, follow the missing-file rule in `RULES.md`. The `generate-code` skill coordinates stage skills rather than duplicating their procedures.

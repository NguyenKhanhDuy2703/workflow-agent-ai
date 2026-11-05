# Project Guide

## Purpose

This repository defines a request-to-delivery workflow for fullstack websites: requirements, design, implementation, verification, and reporting. Read [RULES.md](RULES.md) before starting a task; it defines authority, stop conditions, and document rules.

## Current project state

The repository does not yet contain application source code or design documents. Stage skills and command procedures are present; Python helpers are not yet implemented. Do not describe a planned component as implemented.

| Area | Current state |
| --- | --- |
| Architecture | Not established; record the approved design under `design/docs/system/` when available. |
| Frontend | Not established. |
| Backend | Not established. |
| Database and ORM | Not established. |
| Build and test tools | Not established. |

## Module map

No application modules exist yet. Add a row when a module exists, and update it when its responsibility or location changes.

| Module | Source path | Responsibility | Main dependencies |
| --- | --- | --- | --- |

## Workflow layout

| Path | Purpose |
| --- | --- |
| `design/index.md` | Topics, current versions, and approval status. |
| `design/requirements/<topic>/vN/` | Original input supplied for a topic. |
| `design/docs/system/vN/` | Versioned system design. |
| `design/docs/<topic>/vN/` | Versioned analysis and design for a topic. |
| `.agents/commands/` | Procedures for individual steps. |
| `.agents/skills/` | Procedures that coordinate steps into stages. |

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

When the skill exists, it coordinates the following stages. Pass each stage's output to the next stage. Run only stages relevant to the task, and obey the gates in `RULES.md`.

Analyze a feature in this order: business goal and rules → user/system flow → feature boundary → data ownership and movement → contracts and affected modules. Describe a simple flow as steps; use a sequence or state diagram when ordering, asynchronous messages, or state transitions matter. Derive the implementation architecture from the approved system design and current source. The SpaceLens and project_education repositories are reference examples, not mandatory technology templates.

Each skill stays within its named stage. At the end, report the topic and design version, inputs inspected, work completed, outputs, checks, blockers, and the next permitted stage. The orchestrator passes this report forward; a standalone skill presents it to the user. A report does not authorize the next stage or override a design gate.

**Hard gate:** after `analyze-design`, stop and present the draft design and open questions. Do not start `plan-implementation` until the design is `approved` in `design/index.md` (see `RULES.md`).

| Stage | Read | Produce or update |
| --- | --- | --- |
| Identify topic and version | User request, `RULES.md`, `design/index.md` | Task scope and affected areas. |
| `analyze-design` | `design/requirements/<topic>/vN/`, current system/topic design, relevant source | Draft `design/docs/<topic>/vN/`, open questions, missing-documents report when needed. |
| `plan-implementation` | Approved design, relevant source and tests | Change plan, acceptance checks, affected files and stages. |
| `implement-database` | Approved data design and change plan | Relevant schema, migrations, and tests. |
| `implement-backend` | Approved API/business design and change plan | Relevant contracts, services, controllers, and tests. |
| `implement-frontend` | Approved UI/flow design and change plan | Relevant API mapping, state, UI, and tests. |
| `verify-and-review` | Acceptance checks, changed files, and tests | Test results, diff review, remaining issues, and final report. |

The approved design version is the one recorded in `design/index.md`. If a required skill or command file does not exist, follow the missing-file rule in `RULES.md`. The `generate-code` skill coordinates stage skills rather than duplicating their procedures.

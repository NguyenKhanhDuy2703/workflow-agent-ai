---
name: generate-code
description: Coordinate the request-to-delivery stage skills for one topic, stopping at design approval and resuming from an approved version.
---

# Coordinate request to delivery

Coordinate the stage skills for one fullstack website topic. Read `RULES.md`, `AGENTS.md`, and `design/index.md`; handle separate topics separately.

## Core Capabilities

- Route work from design through planning, affected implementation stages, and verification.
- Enforce the design approval gate and carry each stage's report forward. This skill does not replace command procedures.

## Steps

1. If system design is missing, run [analyze-design](../analyze-design/SKILL.md) for `system` and stop at its draft. If the topic is new or its requirements changed, run the same skill for the topic and stop. If a design is already `draft`, present its questions and wait for approval.
2. When exact system and topic versions are `approved` in the index, run [plan-implementation](../plan-implementation/SKILL.md). Never run it in the same pass that produced a draft.
3. Follow the plan's affected modules: [implement-database](../implement-database/SKILL.md) for storage, [implement-backend](../implement-backend/SKILL.md) for server behavior, and [implement-frontend](../implement-frontend/SKILL.md) for client behavior. Preserve dependency order; skip unaffected stages.
4. Run [verify-and-review](../verify-and-review/SKILL.md) on completed changes.

## Output and Gate

Pass each stage's report, approved versions, changed files, and checks to the next stage. Report after every stage. If required input, a skill/command, or a user decision is missing, stop dependent work. AI or infrastructure work without a matching skill is a reported gap, not backend/frontend work. On resumption, re-read files and status. Never approve, merge, or push automatically.

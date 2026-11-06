---
name: generate-code
description: Coordinate NestJS-centered local code delivery across topics, with concrete stage contracts, discovery, AI or user approval, impact assessment and verification/repair loops.
---

# Coordinate request to delivery

Coordinate the stage skills for one fullstack website work item spanning one or more topics. Read `RULES.md`, `AGENTS.md`, and `design/index.md` if present. Preserve separate topic designs and coordinate their dependencies in the work item.

## Core Capabilities

- Route work from design through planning, affected implementation stages, and verification.
- Enforce recorded approval, preserve exact design versions, and carry each stage's report forward. This skill does not replace command procedures.

For a NestJS target, run or reuse [inspect-nestjs-context](../../commands/inspect-nestjs-context.md) before design/planning and pass its path/symbol map to affected stages. Use [delivery contracts](../../references/nestjs/delivery-contracts.md) for concrete outputs and [verification guidance](../../references/nestjs/verification.md) for evidence. Preserve the target's actual package versions, test runner and approved architecture.

## Steps

1. Run [manage-work-item](../../commands/manage-work-item.md) to create or resume the delivery record. If discovery is missing or outdated, run [discover-project](../../commands/discover-project.md). Resolve linked topics, dependency order, and shared acceptance flows without merging topic designs.
2. If system design is missing, run [analyze-design](../analyze-design/SKILL.md) for `system`. Run it for new or changed topics in dependency order. For an existing draft, run [approve-design-version](../../commands/approve-design-version.md). AI may approve supported designs and continue immediately; pause dependent work for blocking business questions or an explicit user-review request. Approval of one topic does not approve the rest.
3. For code-only defects, preserve the approved behavior and versions. Before switching an existing work item to new intended behavior or versions, run [assess-change-impact](../../commands/assess-change-impact.md), approve the replacements, and update the plan and pinned versions together. Do not switch automatically to a newer draft or approval.
4. Once exact system/topic versions are approved, run [plan-implementation](../plan-implementation/SKILL.md) for affected topics and consolidate their tasks, dependencies and cross-topic acceptance checks in the work item's `plan.md`. Include initial application/build/test setup when source is absent. Persist the `planned` handoff using `manage-work-item`.
5. Follow the plan's affected modules: [implement-database](../implement-database/SKILL.md) for storage, [implement-backend](../implement-backend/SKILL.md) for server behavior, and [implement-frontend](../implement-frontend/SKILL.md) for client behavior. Set `implementing`, preserve dependency order, skip unaffected stages, and persist each handoff. A dependency order need not serialize independent tasks.
6. Set `verifying` and run [verify-and-review](../verify-and-review/SKILL.md), including the work item's cross-topic checks. Consume its classified findings. For implementation defects, set `fixing`, return to the owning implementation skill under the same design, then re-run affected verification and integration checks. For design changes, return through impact assessment, analysis/approval, and re-planning. Resolve local environment issues within scope; report external blockers and continue independent work.
7. Repeat repair and verification while meaningful progress is possible. If a finding persists after two repair attempts without new evidence, or an external dependency prevents progress, record attempts and the next needed input/action and stop dependent retries as `blocked`. Mark `done` only when required local checks and acceptance flows pass with no blocking finding. Use `manage-work-item` and [report-result](../../commands/report-result.md) for the final local delivery record.

## Output and Gate

Persist each stage's report, exact approved versions, changed files, findings and checks in the work item. If required input, a skill/command, or a business decision is missing, stop dependent work. AI processing or infrastructure work without a matching skill is a reported gap, not backend/frontend work. On resumption, re-read the work item, files and status. AI design approval is allowed under `RULES.md`; push, merge and deployment require separate explicit instructions. Completion means changed code verified locally.

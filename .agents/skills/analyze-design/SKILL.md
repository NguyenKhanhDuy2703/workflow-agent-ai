---
name: analyze-design
description: Analyze a topic and record supported design approval; for NestJS, resolve concrete operation, DTO, access, data and acceptance contracts before implementation.
---

# Analyze design

Analyze one topic and publish a traceable design. Read `RULES.md`; complete project discovery and analyze `system` first if its design is missing. Editing workflow procedures alone does not bootstrap an application design.

## Core Capabilities

- Turn original input into business rules, flow, module boundary, data ownership, contracts, and acceptance criteria.
- Expose missing documents and conflicts without inventing decisions. This skill does not plan or implement source changes.

For NestJS tasks, run or reuse [inspect-nestjs-context](../../commands/inspect-nestjs-context.md) and use the applicable [delivery contracts](../../references/nestjs/delivery-contracts.md). Resolve transport/DTO/access/response/data/side-effect/acceptance decisions, with source references or explicit not-applicable reasons. A source example does not decide a missing business policy.

## Steps

1. For initial system analysis or changed project context, run [discover-project](../../commands/discover-project.md). Run [check-input](../../commands/check-input.md) for the topic, original requirements, and required documents. If no usable input exists, report what is missing and stop dependent work.
2. Run [read-design](../../commands/read-design.md) to identify exact versions and decisions to preserve or revise; missing designs are expected during initial creation. For a change to existing intended behavior, run [assess-change-impact](../../commands/assess-change-impact.md) and finalize its assessment before adopting a replacement.
3. Run [extract-requirements](../../commands/extract-requirements.md). Organize the draft as **business rules → flow → feature boundary → data ownership → contracts and affected modules**. Use a sequence or state diagram when ordering or transitions need one.
4. Run [compare-source](../../commands/compare-source.md) if source exists; otherwise record that this step was skipped.
5. Run [report-gaps](../../commands/report-gaps.md). Separate implementation defects from design changes and unresolved requirement conflicts. Ask for missing business decisions; AI may resolve supported technical proposals within scope and record its rationale.
6. Run [publish-design-version](../../commands/publish-design-version.md) when sourced input supports a meaningful draft, then [approve-design-version](../../commands/approve-design-version.md). Retain `draft` for blocking gaps or explicit user review; otherwise AI may approve and hand off immediately. For initial system design, define the application structure and local build/test setup needed before feature work.

## Output and Gate

Report topic/version, design path, sources, flow, module/data/contract decisions, acceptance criteria, gaps, and approval decision/evidence. Planning requires exact versions marked `approved` in `design/index.md`. A standalone invocation ends after this report; the orchestrator may continue in the same run after approval.

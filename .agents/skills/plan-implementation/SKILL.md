---
name: plan-implementation
description: Plan file/symbol changes and acceptance checks for an approved topic, including NestJS DTO/service/controller/module and persistence dependencies when applicable.
---

# Plan implementation

Plan source changes for one approved topic without editing application code.

## Core Capabilities

- Map approved acceptance criteria to affected modules, files, contracts, and tests.
- Order database, backend, and frontend work while preserving the approved architecture.

For NestJS, run or reuse [inspect-nestjs-context](../../commands/inspect-nestjs-context.md) and the [file-level delivery contract](../../references/nestjs/delivery-contracts.md). Each task names an AC, owner, exact file/symbol, dependency and required local command/evidence level. Include module/provider wiring and affected API consumers rather than only controller/service edits.

## Steps

1. Run [read-design](../../commands/read-design.md) for the work item's pinned versions, or exact approved versions in a standalone task. When re-planning a design change, explicitly pass the approved target-version mapping recorded in its impact assessment; existing pins remain the execution baseline until the adoption handoff. Collect flow, boundaries, data, contracts, and acceptance criteria. Stop if a required decision is missing.
2. Run [compare-source](../../commands/compare-source.md) to locate current behavior and tests; explicitly skip source comparison when source does not exist. Classify contradictions: plan fixes for clear implementation defects under the existing design; assess impact and obtain approved replacements before planning changed intent.
3. Run [plan-change](../../commands/plan-change.md) to map acceptance criteria to files, modules, dependencies, implementation order, and required/optional local checks. Include initial application and build/test setup for a new project. Keep domain boundaries in a modular monolith and explicit contracts between separate services.
4. When part of a work item, save/consolidate the plan in its `plan.md`, preserving tasks for other topics and recording cross-topic dependencies and acceptance checks. For version adoption, save the revised plan and target versions as the new pins in one recorded handoff before implementation resumes; do not execute a plan whose version references disagree with its pins.

## Output and Gate

Report the exact approved versions, affected modules and layers, ordered changes, acceptance mapping, tests, and blockers. Mark any area without a matching implementation skill as unsupported; do not route it into another skill.

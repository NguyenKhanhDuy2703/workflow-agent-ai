# plan-change

Map approved acceptance criteria to an ordered implementation plan.

## Input
Exact approved topic/system versions, work item when present, source comparison or explicit no-source result, module map/tests if present, and requested scope.

## Gate
The relevant versions are `approved` in `design/index.md`; stop if the required UI, data, or API design is missing.

## Steps
1. Map each acceptance criterion to affected modules, data, contracts, and database/backend/frontend work. For NestJS apply the [file-level delivery contract](../references/nestjs/delivery-contracts.md): each task has an owner, create/change/remove/verify action, exact file/symbol, dependency/handoff, and required command with cwd/evidence level/expected result. Name unsupported areas rather than forcing them into these three skills.
2. Order changes by actual dependencies, including cross-topic edges: storage before code that needs it, producer contracts before dependent integration, and state interfaces before dependent UI. Independent work need not be serialized. Preserve domain boundaries and explicit integration contracts.
3. Record expected file areas, migration/compatibility concerns and open decisions. Include initial application structure and local build/test setup for a project without source, using the approved system design and supported implementation skills. Plan code corrections under the existing approved behavior; a design change requires impact assessment and an approved replacement before planning that change.
4. Map each acceptance criterion to evidence, marking required and optional local checks. For NestJS include changed module/DI/configuration, DTO/request access/status behavior, service invariants and Prisma migration/constraint checks at their actual layers. Include cross-topic end-to-end success/failure flows and affected clients where applicable. Separate topic tests alone do not prove the shared flow; use [verification guidance](../references/nestjs/verification.md) to distinguish evidence levels.
5. Save/consolidate the plan as the work item's `plan.md` when present, with exact approved version references and ordered tasks. Do not silently switch pinned versions; update them only after impact assessment and approval when adopting a replacement.

## Output
A change plan tied to exact approved versions, with affected modules/layers, dependencies and ordered tasks, contract handoffs, required/optional local checks including cross-topic acceptance, and unsupported areas.

## Done when
Each planned change traces to approved design and the next stage can act without choosing the feature's intended behavior.

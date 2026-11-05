# plan-change

Map approved acceptance criteria to an ordered implementation plan.

## Input
Approved topic and system design, source comparison, module map, existing tests, and the requested scope.

## Gate
The relevant versions are `approved` in `design/index.md`; stop if the required UI, data, or API design is missing.

## Steps
1. Map each acceptance criterion to affected modules, data, contracts, and database/backend/frontend work. Name other affected areas rather than forcing them into these three.
2. Order dependent changes: storage before its consumers, producer contract before its consumers, and state before UI. Preserve domain boundaries in a modular monolith and explicit integration contracts between separate services.
3. Record expected file areas, tests, migration/compatibility concerns, and open decisions. If source contradicts approved design, stop the affected plan and report the conflict.

## Output
A change plan tied to exact approved versions, with affected modules/layers, ordered tasks, contract handoffs, acceptance checks, tests, and unsupported areas.

## Done when
Each planned change traces to approved design and the next stage can act without choosing the feature's intended behavior.

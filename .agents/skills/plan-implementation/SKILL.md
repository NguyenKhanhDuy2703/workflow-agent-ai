---
name: plan-implementation
description: Plan source changes and verification for one topic whose relevant design version is approved.
---

# Plan implementation

Plan source changes for one approved topic without editing application code.

## Core Capabilities

- Map approved acceptance criteria to affected modules, files, contracts, and tests.
- Order database, backend, and frontend work while preserving the approved architecture.

## Steps

1. Run [read-design](../../commands/read-design.md) to collect approved flow, module boundaries, data, contracts, and acceptance criteria. Stop if a required UI, data, or API decision is missing.
2. Run [compare-source](../../commands/compare-source.md) to locate current behavior and tests. Stop the affected plan if source contradicts approved design.
3. Run [plan-change](../../commands/plan-change.md) to map acceptance criteria to files, modules, dependencies, implementation order, and checks. Keep domain boundaries in a modular monolith and explicit contracts between separate services.

## Output and Gate

Report the exact approved versions, affected modules and layers, ordered changes, acceptance mapping, tests, and blockers. Mark any area without a matching implementation skill as unsupported; do not route it into another skill.

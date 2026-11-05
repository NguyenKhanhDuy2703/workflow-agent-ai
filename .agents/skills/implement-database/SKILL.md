---
name: implement-database
description: Implement approved data-model and migration changes when the change plan affects persistent storage.
---

# Implement database changes

Implement the approved persistence portion of a fullstack website change.

## Core Capabilities

- Update schema or ORM definitions and migrations within the project's data ownership boundaries.
- Check compatibility and persistence behavior. Service and API changes belong to the backend skill.

## Steps

1. Confirm exact plan versions remain `approved` in `design/index.md`; read approved data ownership, current schema, and migration history. Stop if persistence behavior is undefined.
2. Run [update-orm](../../commands/update-orm.md) for the planned schema and migration. Stop on unresolved data-loss or compatibility decisions.
3. Run [run-relevant-tests](../../commands/run-relevant-tests.md) for the changed persistence behavior.

## Output and Gate

Report changed files, migration order, compatibility impact, test results, blockers, and the data interface the backend must consume.

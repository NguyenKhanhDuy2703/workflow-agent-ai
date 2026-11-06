---
name: implement-database
description: Implement approved data-model and migration changes when the change plan affects persistent storage.
---

# Implement database changes

Implement the approved persistence portion of a fullstack website change.

## Core Capabilities

- Update schema or ORM definitions and migrations within the project's data ownership boundaries.
- Check compatibility and persistence behavior. Service and API changes belong to the backend skill.

For NestJS/Prisma, use the actual schema, client service and migration history established by [inspect-nestjs-context](../../commands/inspect-nestjs-context.md). Follow the database handoff in [delivery contracts](../../references/nestjs/delivery-contracts.md) and [verification guidance](../../references/nestjs/verification.md); do not infer real migration/transaction evidence from mocks or replace existing persistence conventions with the reference's versions.

## Steps

1. Confirm the exact design versions referenced by the plan/work item remain `approved` in `design/index.md`; read approved data ownership, schema and migration history if present. For initial setup, create persistence files only as specified by the approved design/plan. Stop if persistence behavior is undefined. Verification repairs use the same versions unless an assessed design change was approved and re-planned.
2. Run [update-orm](../../commands/update-orm.md) for the planned schema and migration. Stop on unresolved data-loss or compatibility decisions.
3. Run [run-relevant-tests](../../commands/run-relevant-tests.md) for the changed persistence behavior.

## Output and Gate

Report changed files, migration order, compatibility impact, test results, blockers, and the data interface the backend must consume.

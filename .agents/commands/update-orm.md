# update-orm

Update persistence schema and migration for approved data changes.

## Input
Approved data design, change plan, current persistence stack, schema/ORM files, migration history, and relevant tests.

## Gate
The plan requires a storage change and the project's persistence approach is established.

## Steps
1. Compare approved ownership/invariants with schema, relations, unique/index/default/null/mapped-name definitions and migration history. For NestJS/Prisma, use actual paths/client version from context and the [database delivery contract](../references/nestjs/delivery-contracts.md); do not assume TypeORM or introduce a second Prisma client service.
2. Implement the smallest approved schema delta and migration using existing conventions. Inspect SQL/order and compatibility with existing rows, including backfill, defaults, constraint failures and delete behavior. Preserve applied migration history and table/column mappings.
3. Record client regeneration and dependent service/query changes. Select schema validation, generation and real migration/constraint checks from [verification guidance](../references/nestjs/verification.md). Use tools compatible with the installed Prisma major; `generate` is not evidence that SQL was applied.
4. Inspect the identified disposable local DB and fixture/cleanup plan before any command that writes data. Do not use reset/`db push`/seed as an automatic substitute for migration verification. Stop dependent changes for unresolved data-loss/irreversible decisions or missing required DB evidence.
5. Update meaningful persistence checks/fixtures. Distinguish schema/SQL smoke checks, mocked-client tests and real constraint/transaction evidence; avoid changing counts or snapshots merely to conceal schema/history mismatches.

## Output
Schema/SQL/test delta, migration/backfill order and compatibility, generated-client needs, local commands/database evidence limits, and dependent service/query handoff.

## Done when
The schema and migration express the approved data design and relevant verification is ready to run.

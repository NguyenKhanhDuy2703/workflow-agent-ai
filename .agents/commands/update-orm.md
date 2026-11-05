# update-orm

Update persistence schema and migration for approved data changes.

## Input
Approved data design, change plan, current persistence stack, schema/ORM files, migration history, and relevant tests.

## Gate
The plan requires a storage change and the project's persistence approach is established.

## Steps
1. Compare approved data ownership and model with current schema; identify the smallest change within the owning module.
2. Update schema/ORM definitions and create a migration using project conventions. Inspect ordering and compatibility with existing data.
3. Update affected persistence tests or fixtures. Stop if data loss or an irreversible migration is required but not decided in approved design.

## Output
Changed schema, migration, and test/fixture files; migration order, risks, and the data interface for backend consumers.

## Done when
The schema and migration express the approved data design and relevant verification is ready to run.

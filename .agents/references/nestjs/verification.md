# NestJS local verification

Read actual scripts and test bodies. The reference uses npm, `tsx` and `node:test`; other targets may differ. Do not install Jest, Supertest or `@nestjs/testing` just to fit a template.

## Evidence levels

| Level | Establishes | Cannot establish alone |
| --- | --- | --- |
| Static/build | Types, imports/declarations and compilation | DI, reachable routes, executed guards/pipes or DB behavior |
| Unit/service with doubles | Executed production methods and branch/interaction outcomes | HTTP pipeline, real constraints/concurrency or SQL rollback |
| Nest composition | Resolution of actual modules/providers and reachability | Full external behavior or production configuration |
| HTTP/request path | Routing, validation, guards, status and serialized response under relevant bootstrap config | Real persistence if the client is mocked |
| Isolated DB | Migrations, constraints, queries/transactions and persistence invariants in the designated DB | Browser behavior or guards unless included |
| Connected client/cross-topic | The connected API/client/domain journey exercised | Layers excluded or mocked by the harness |

Label actual executed layers, not filenames like `integration`/`e2e`. Report doubles. Source-text checks prove structure only; simulations not calling production logic cannot prove that logic was fixed.

## Select checks by change

- Service rule: execute the production method for success and relevant invalid/denied/state-conflict/regression paths. Test repetition/concurrency when the invariant depends on it.
- DTO/controller/auth: exercise the affected request through relevant actual pipes/guards/filter configuration. Include malformed input, extra fields when rejected, absent credentials, denied policy and success where applicable. Bypassing guards cannot prove access control.
- Module/provider/import/config: include composition/boot evidence. Use available tools or an existing harness; a local Node/Nest harness can suffice without new test frameworks. Overrides must not erase the DI edge being checked.
- Prisma invariant: validate schema, regenerate the client when needed, inspect SQL and run required migration/constraint/transaction checks on an identified disposable local database. A mocked `$transaction` proves interaction, not atomicity.
- API used by clients: inspect affected consumers and verify payload/error/credential mapping and relevant tests/builds. A required connected flow cannot be replaced by independent mocks.

Select levels from approved acceptance criteria and plan; small changes need not run every level. If required evidence is unavailable, report `not-run` and a blocker rather than substituting weaker evidence.

## Reference commands

These are inspected script examples, not commands executed by this workflow. Resolve the target checkout and cwd first. Inspect tests before running; some require PostgreSQL/config/fixtures and write data.

| cwd | Command | Purpose/limit |
| --- | --- | --- |
| `MODULE_BE` | `npm run build` | Existing `nest build`; required compilation evidence for backend TypeScript changes. |
| `MODULE_BE` | `npx --no-install tsx --test test/auth-session.service.spec.ts` | Focused existing service test example; select an actual affected file. Uses local tooling without installation. |
| `MODULE_BE` | `npm test` | Existing `tsx --test "test/**/*.spec.ts"`; broader suite when required/justified. Inspect DB dependencies first. |
| `MODULE_BE` | `npm run test:e2e` | Runs `tsx test/backend-e2e-matrix.test.ts`; directly constructs services with Prisma and seeded personas, writes/cleans data. Not proof of HTTP guards/pipes. Requires an identified disposable local DB. |
| `MODULE_BE` | `npx --no-install prisma validate` | Schema validation with local version/config; not proof of migration application. |
| `MODULE_BE` | `npx --no-install prisma generate` | Local client generation for approved schema changes; inspect generators first. Not a migration. |
| `MODULE_FE` | `npm test` / `npm run build` | Existing Vitest and TypeScript/Vite scripts when learner client is affected. |
| `MODULE_ADMIN` | `npm test` / `npm run build` | Existing Vitest and TypeScript/Vite scripts when admin client is affected. |

Do not invent backend `lint`, `test:unit` or `test:integration` scripts. Observed backend has no lint script; `format` rewrites files and is not a read-only check. Re-read manifests if they change.

Select migration generation/application commands compatible with installed Prisma, existing history, approved plan and disposable test DB. Verify target without logging credentials. Do not default to seeds/reset/`db push`/migrations on shared or unknown databases. A README setup shortcut is not migration evidence.

## Result record

Record AC/check ID, cwd, exact command, environment/fixtures, executed layers/mocks, pass/fail/not-run, observable result and unverified layers in the work-item verification report when present. Exclude secrets/connection strings.

After repair, re-run failed/affected integration checks and retain still-valid unchanged evidence. Local completion requires planned evidence to pass; it does not claim deployment or production acceptance.

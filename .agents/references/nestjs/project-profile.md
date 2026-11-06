# NestJS project profile

Use this profile for a NestJS backend. NestJS is this workflow's primary backend stack; approved architecture and actual target source take precedence over reference examples.

## Evidence and scope

Reference: [project_education](https://github.com/NguyenKhanhDuy2703/project_education). Inspected on 2026-11-06 using the matching local checkout `D:/Projects/study-web`; its origin points to that repository, and its `dev` ref identifies `8d253c9fdd5b03030f26107ce2c1775c13cfebcd`. These findings describe files read from that checkout; remote branches/local edits may differ. Re-read target files before applying them. The reference application was not modified or executed.

This workflow repository contains procedures, not the reference application. Do not add reference modules to its application module map or claim their tests passed here.

## Observed structure

Paths are relative to the reference root. Its [backend source tree](https://github.com/NguyenKhanhDuy2703/project_education/tree/dev/MODULE_BE) is a navigation aid, not a version lock.

| Concern | Evidence paths | Finding |
| --- | --- | --- |
| Stack/tooling | `MODULE_BE/package.json`, `nest-cli.json`, `tsconfig.json` | NestJS/Express, TypeScript decorators, Swagger compiler plugin, npm scripts. Manifest ranges include NestJS 12 and Prisma 6; inspect lockfile/installed versions rather than requiring these versions elsewhere. |
| Composition | `MODULE_BE/src/app.module.ts`, `src/modules/groups/groups.module.ts`, `src/modules/auth/auth.module.ts` | Domain modules register controllers/providers and expose dependencies through imports/exports. Verify root reachability. |
| Bootstrap | `MODULE_BE/src/main.ts`, `src/configs/app.config.ts` | Configured global prefix (default `api/v1`), credentialed CORS, cookie parser, global validation pipe, exception filter and Swagger. |
| DTOs | `MODULE_BE/src/modules/groups/dto/create-group.dto.ts`, `src/modules/auth/auth.dto.ts` | Concrete classes, `class-validator` rules and Swagger metadata. DTO location differs by module. |
| Authentication | `MODULE_BE/src/modules/auth/jwt.strategy.ts`, `src/common/guards/jwt-auth.guard.ts` | Passport JWT accepts `accessToken` cookie or Bearer token; validated principal includes `userId` and role. Do not assume `req.user.id`. |
| Authorization | `MODULE_BE/src/common/guards/roles.guard.ts`, `resource-owner.guard.ts`, `src/modules/entitlements/guards/feature-entitlement.guard.ts` | Role, ownership and feature entitlement checks are distinct; policy metadata requires matching guard wiring. |
| Persistence | `MODULE_BE/prisma/schema.prisma`, `prisma/migrations/`, `src/prisma/prisma.service.ts`, `prisma.module.ts` | PostgreSQL, schema and SQL migration history; injectable client service with lifecycle hooks. Preserve mappings, relations, constraints and client ownership. |
| Use cases | `MODULE_BE/src/modules/groups/groups.service.ts`, `src/modules/billing/billing.service.ts` | Injectable services use Prisma directly. Billing demonstrates transactions and conditional updates. A repository layer is not an existing universal convention. |
| Tests | `MODULE_BE/package.json`, `test/auth-session.service.spec.ts`, `test/session-security.spec.ts`, `test/upgrade-lifecycle-integration.spec.ts`, `test/backend-e2e-matrix.test.ts` | `tsx`/`node:test`, service/guard tests and doubles, plus a DB-dependent service matrix. Names alone do not prove HTTP/DB coverage. |
| Consumers | `MODULE_FE/src/services/api.client.ts`, `MODULE_ADMIN/src/services/api.client.ts` | Separate React clients use Axios base URLs, credentials and refresh handling; their refresh implementations differ. |

## Adaptation rules

- Read target manifests/lockfile, adapter/bootstrap, one complete nearby module, persistence setup and representative tests before selecting paths or commands. Do not upgrade packages while adopting this workflow.
- Role values, admin bypasses, content states and response shapes in the example are observations, not approved business policy for another project.
- The reference enables `whitelist`, `forbidNonWhitelisted` and `transform`. Check target options; TypeScript types and Swagger annotations do not provide runtime validation.
- Do not presume a global success envelope, global auth guard, Jest, Supertest, `@nestjs/testing`, a lint script or shared frontend contracts. Establish each from source/manifests.
- Preserve actual cookie behavior, filters/interceptors and client unwrapping unless the approved change intentionally alters them.
- Use the installed Prisma major's API. Newer online docs are not permission to replace the reference's Prisma 6 `$transaction` client, generator, datasource or migrations.
- For grading tasks, keep production persistence separate from PGlite/other sandboxes. This domain-specific boundary is not a generic persistence pattern.

## Read next

- Design/approval and outputs: [delivery contracts](delivery-contracts.md).
- Commands and evidence levels: [verification](verification.md).
- New target: [inspect-nestjs-context](../../commands/inspect-nestjs-context.md).

Framework semantics were cross-checked against official [controllers](https://docs.nestjs.com/controllers), [validation](https://docs.nestjs.com/techniques/validation) and [testing](https://docs.nestjs.com/fundamentals/testing) documentation. Use APIs compatible with installed versions.

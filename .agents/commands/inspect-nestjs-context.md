# inspect-nestjs-context

Identify the target NestJS stack and concrete integration points before designing or editing it.

## Input
Target repository/path, scope, approved system design/discovery when present, manifests/lockfile, representative source and tests.

## Gate
For a NestJS task before analysis/planning/implementation, or when previous context no longer matches. Reuse current source-backed findings. No source edits in this command.

## Steps
1. Read the [project profile](../references/nestjs/project-profile.md). Locate the backend root; inspect dependency/lockfile versions, scripts, Nest CLI/TypeScript settings, bootstrap and root module. Do not assume `MODULE_BE` or reference dependency versions. For no-source projects, skip unavailable source inspections and report proposed bootstrap outputs under step 5.
2. Trace a nearby use case through controller/DTO, service/providers, module imports/exports and data client. Identify prefix, validation, exception/response handling, config validation and runtime adapter behavior relevant to the task.
3. Trace affected authentication, role/ownership/tenant/feature checks, principal shape and registration. Locate persistence/schema/migration paths. Inspect representative test bodies, scripts and environment needs; distinguish doubles from HTTP/DB evidence.
4. Locate affected learner/admin/service consumers; record base URL/prefix, credentials, payload/error decoding and refresh behavior relevant to the change.
5. Report concern, exact path/symbol, observed behavior/version, source and gap in a compact map. Persist in discovery/work-item context when available. For no-source projects, label proposed paths/dependencies/setup as proposals for system approval rather than existing implementation.

## Output
Source-backed stack/module/bootstrap/access/persistence/test/consumer map, actual local commands/prerequisites, and gaps blocking dependent work.

## Done when
The caller can name concrete files and conventions without importing unverified reference assumptions.

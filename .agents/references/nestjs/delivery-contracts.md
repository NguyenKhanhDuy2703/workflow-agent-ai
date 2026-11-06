# Concrete NestJS delivery contracts

Apply only sections relevant to the change. Record explicit not-applicable reasons rather than inventing endpoints, UI work, persistence or policies. These are minimum decision contents, not a requirement to create many files.

## Design ready for approval

Resolve these decisions for each affected endpoint/backend operation. Missing business policy blocks that operation; source-supported technical choices may be recorded and approved by AI.

| Decision | Required content |
| --- | --- |
| Behavior/owner | Requirement IDs/sources, actor and outcome, owning module/service, collaborators and scope exclusions. |
| Transport | Method, controller path plus actual global prefix/versioning, service operation and status codes. For a worker/event, record trigger, payload and retry behavior instead of inventing HTTP. |
| Request | DTO/field table: type, required/optional, null/omission behavior, bounds/enums, nested/array rules, conversions, path/query rules and unknown-field policy. |
| Access | Public/authenticated, credential transport, principal identity field, role, ownership/tenant and feature/subscription rules where applicable; actual guards/decorators and registration. |
| Response/errors | Success status/payload example, exposed fields, error statuses/shapes/conditions, filters/interceptors and affected client decoding. Avoid default serialization of sensitive Prisma records. |
| Data/invariants | Owning models/relations, unique/index/null/default changes, reads/writes, atomicity, concurrency/repeated-request behavior, migration/backfill and compatibility where relevant. |
| Side effects | Audit/notification/event effects, timing relative to commit and failure/retry behavior when relevant. External effects do not roll back merely because SQL does. |
| Acceptance | Stable AC IDs with actor/preconditions, request/action, expected status/result, state change/no-change, denied/error paths and cross-topic scenarios. |

A read-only endpoint may mark transactions/side effects not applicable. For a bug, reference unchanged approved decisions and identify the violated invariant instead of rewriting the design.

Approval requires applicable rows resolved, source references separating confirmed input from AI decisions, and checks capable of detecting intended behavior. Compilation alone is not a behavior check. Do not add policies merely because the reference has them.

## File-level plan

Each task identifies:

- Requirement/AC ID and exact approved design versions.
- Owning skill and create/change/remove/verify action, repository-relative file and important symbol/model. Label proposed paths for new modules.
- Prerequisites/handoff: DTO shape, service signature, exported provider, schema/client delta or consumer. Separate actual dependencies from independent tasks.
- Required local command/check, cwd, prerequisites, evidence level and expected behavior/result. Identify DB dependencies before running tests.

In the reference layout, a feature may affect `MODULE_BE/prisma/schema.prisma`, a migration, `src/modules/<domain>/dto/`, service/controller/module, root module imports and `test/`. Create only what the scope needs. Change `MODULE_FE` or `MODULE_ADMIN` only when that consumer is affected.

Order schema/client changes before code that needs them and interfaces before consumers; verify provider/controller wiring after composition. Avoid unplanned architecture or test-runner migrations.

## Stage handoffs

| Step | Output | Done when |
| --- | --- | --- |
| Context | Root/version/script/bootstrap/module/access/persistence/test/consumer map with sources/gaps | Actual paths and conventions are established; missing source is explicit. |
| Design/approval | Applicable decisions above, AC IDs, gaps and approval evidence | Coding will not require inventing business behavior. |
| Plan | File/symbol tasks, owners, dependencies and check mapping | Each stage can act on explicit inputs and approved versions. |
| Database | Schema delta, SQL/order, backfill/compatibility, generated-client needs and limits | Model/history agree and required migration evidence exists. |
| Contract/DTO | Changed fields, runtime rules, success/error shape and consumers | Transport and clients have an unambiguous interface. |
| Service | Use case, principal inputs, invariants, transactions/side effects and checks | Real service behavior satisfies applicable ACs. |
| Controller | Method/path, validation/access wiring, service call, statuses/payload and evidence | Required transport behavior is connected and verified. |
| Module/config | Providers/imports/exports/root reachability and relevant config | A composition/boot check resolves intended wiring. |
| Verification | AC-to-command results with unit/service/HTTP/DB/UI evidence separated, findings | Required behavior/integration evidence passes with no blocker. |

A build does not prove DI resolution. A direct service constructor test does not prove routes, guards, DTO pipes or SQL rollback. See [verification](verification.md).

## Example: add a member to an IAM group

This illustrates analysis and planning, not approval of a new policy or a requested app change.

1. Inspect existing group controller/service/module, member DTO, Prisma relation/unique key, roles policy and tests. Reuse the use case if already implemented.
2. Resolve route/status, actor identity, permitted role/ownership, member eligibility, missing IDs, duplicate/repeated-request behavior and audit/entitlement effects from requirements. Ask for unresolved business choices.
3. Map decisions to DTO rules, service/constraints, controller guards/statuses and module dependencies. Skip schema work if the existing model suffices.
4. Plan permitted success, unauthenticated/denied access, malformed input, missing resources and approved duplicate behavior. Link entitlement checks only if membership is intended to affect them.
5. Use real service methods with doubles for use-case rules, request-path evidence for changed access/validation, and isolated-DB evidence for new uniqueness/transaction claims. Do not label a mocked service journey HTTP/DB end-to-end coverage.

# implement-service

Implement approved backend business behavior.

## Input
Approved business rules, change plan, current service/domain code, relevant contracts, and tests.

## Gate
The plan changes backend business behavior and required rules are defined.

## Steps
1. Locate the owning domain service and approved dependencies. For NestJS, read the nearby injectable/provider/client patterns and applicable [delivery contracts](../references/nestjs/delivery-contracts.md). Use existing injected providers; do not impose a repository/CQRS layer or bypass another module's contract.
2. Implement the approved use case, receiving the actual authenticated principal/actor fields needed by policy. Do not trust client-supplied actor, owner or privileged state fields. Preserve required ownership/tenant/entitlement and legal state-transition checks at the appropriate boundary.
3. Implement defined reads/writes, missing-resource/conflict behavior, explicit response projection and side effects. For Prisma, use the installed client/service, approved transaction boundary and transaction client throughout the atomic unit. Use the approved uniqueness/conditional-update/concurrency strategy; read-then-write checks alone are not proof against races.
4. Keep audit/notification/event behavior consistent with the approved commit/failure semantics. Reuse existing error mapping; do not leak raw database errors or return fields merely because Prisma selected them. Keep cookies, HTTP response handling and transport parsing in entrypoints.
5. Add or update focused checks that execute production service methods for relevant ACs and regression paths. State mocked layers and use planned real-DB checks for claims about SQL constraints/atomicity. Report undefined business rules instead of silently choosing them.

## Output
Changed files/symbols, AC coverage, service/principal interface, invariants/transaction/side-effect behavior, result/error projection, checks with evidence limits, and unresolved decisions.

## Done when
The service behavior matches approved rules and is ready for controller integration and relevant tests.

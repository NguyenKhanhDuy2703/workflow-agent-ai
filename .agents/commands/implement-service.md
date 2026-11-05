# implement-service

Implement approved backend business behavior.

## Input
Approved business rules, change plan, current service/domain code, relevant contracts, and tests.

## Gate
The plan changes backend business behavior and required rules are defined.

## Steps
1. Locate the responsible domain module and its approved dependencies; do not bypass another module's contract.
2. Implement approved business behavior, failure cases, and persistence or event interactions where specified. Keep transport details in entrypoints.
3. Add or update focused tests that verify the acceptance criteria. Report any rule that cannot be derived from approved design.

## Output
Changed service/domain code and tests, behavior exposed to entrypoints, and unresolved decisions.

## Done when
The service behavior matches approved rules and is ready for controller integration and relevant tests.

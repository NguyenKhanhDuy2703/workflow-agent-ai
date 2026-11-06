# run-relevant-tests

Run checks that cover the changed behavior and record results.

## Input
Changed areas, approved acceptance criteria, planned required/optional checks including cross-topic flows, project test configuration, and available local test commands.

## Gate
An implementation stage needs focused feedback or final verification needs evidence.

## Steps
1. Run planned required local checks, including cross-topic acceptance where applicable. For NestJS read the [verification guidance](../references/nestjs/verification.md), actual scripts and selected test setup before execution. Identify tool versions, cwd, config/fixture needs, database targets and mocked layers; do not assume Jest or invented scripts. Preserve required/optional distinctions and broaden only for concrete integration risk or a project gate.
2. Run checks and capture AC ID, exact command/cwd, affected module, result, observed behavior and failure details. Include integration paths where data/contracts cross boundaries. Label static/build, unit/service, composition, HTTP, real-DB and client evidence honestly; tests named `e2e` may exercise only services. Do not rewrite source/snapshots merely to pass.
3. If a check cannot run, state why and what remains unverified. A required unavailable or failed check blocks local completion. After a repair, re-run affected checks and integration paths; reuse still-valid evidence for unchanged scope instead of repeating unrelated checks.

## Output
Local test/check commands by module and acceptance criterion, required/optional flags, pass/fail/not-run results, cross-topic evidence, and actionable failure details.

## Done when
The caller has accurate verification evidence for the affected scope, including any limits.

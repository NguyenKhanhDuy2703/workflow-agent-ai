# run-relevant-tests

Run checks that cover the changed behavior and record results.

## Input
Changed areas, approved acceptance criteria, project test configuration, and available test commands.

## Gate
An implementation stage needs focused feedback or final verification needs evidence.

## Steps
1. Select the smallest checks that meaningfully cover the changed behavior, then include broader checks only when a concrete integration risk or project gate calls for them.
2. Run the selected checks and capture exact command, affected module, result, and relevant failure details. Include integration checks where data or contracts cross module boundaries. Do not rewrite source or snapshots just to make a check pass without examining the cause.
3. If a check cannot run, state why and what remains unverified.

## Output
Test/check commands by module, pass/fail/not-run results, and actionable failure details.

## Done when
The caller has accurate verification evidence for the affected scope, including any limits.

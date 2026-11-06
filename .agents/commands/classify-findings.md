# classify-findings

Turn verification results into repair routes without performing the repairs.

## Input
Test results and diff findings, pinned designs, acceptance criteria, change plan, work item, and prior repair attempts when present.

## Gate
Verification has produced results, including a failed or unavailable required check.

## Steps
1. Give each actionable finding an ID, evidence/location, affected acceptance criterion, impact and blocking status. A required local check that failed or could not run blocks completion; distinguish this from an optional unrun check.
2. Route implementation defects to the owning database/backend/frontend skill under the same design. Route intended behavior changes through impact assessment, analysis/approval, and re-planning. Route environment blockers to a concrete local remedy within scope or the exact external input/action needed. Missing skills remain explicit gaps.
3. Identify affected checks and integration paths to re-run after a repair. Record attempt history and whether new evidence exists. If the same finding persists after two repair attempts without new evidence, or an external dependency prevents progress, stop dependent retries and record the blocker and next action.
4. Persist results in the work item's verification report when present. Report a structured handoff to the orchestrator; a standalone invocation ends here and does not start implementation.

## Output
Classified findings with repair owners/routes, blocking status, re-verification scope, attempts and next actions, or an explicit no-findings result.

## Done when
Each result can be routed without silently changing approved behavior or claiming that unavailable required evidence passed.

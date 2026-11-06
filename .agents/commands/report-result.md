# report-result

Report the work, verification, blockers, and next permitted action.

## Input
Task scope, work item when present, exact design versions and approval state, changed files, available test/review evidence, and unresolved questions. Draft analysis and early stops need not have approved versions or test results; report those as pending or not applicable.

## Gate
At the end of verification or when a stage stops before completion.

## Steps
1. State the stage or command completed, work item when present, topics, exact design versions/statuses, scope, and actual execution state.
2. List inputs inspected, files changed, outputs for the next stage, checks and results, findings, and work not completed. Explain any stop condition and exact decision or input needed to continue.
3. Report local completion only when code meets acceptance criteria, all required local checks including cross-topic flows pass, and blocking findings are resolved. Otherwise report partial work, repair routes, or blockers. Optional unrun checks retain their stated limits; failed or unavailable required checks prevent `done`.
4. Link persisted handoff/verification evidence in the work item when present. Do not merge, push, deploy, or change design approval merely as part of reporting; design approval uses its dedicated command. For documentation-only work, state the document checks performed without implying application verification.

## Output
A concise stage report with evidence, handoff output, blockers, and next permitted action.

## Done when
The user can tell what changed, what was verified, and what remains open.

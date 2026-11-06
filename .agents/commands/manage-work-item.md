# manage-work-item

Create or update the execution record connecting one delivery request to its topic designs.

## Input
Request/scope, related topics, design index if present, stage reports, existing work item if resuming, and any dependency or acceptance evidence.

## Gate
At the start of application delivery, after a stage handoff, when a blocker changes, and before reporting completion. A workflow-procedure edit alone does not require application delivery records.

## Steps
1. Reuse the work item for the request or create a kebab-case work ID and `work/items/<work-id>/work-item.md`. Record the original request reference, scope/exclusions, linked topics, and exact system/topic design versions with status. Initial analysis may list unresolved versions; planning cannot.
2. Record dependency edges and their execution order, including any cross-topic contracts. Give acceptance criteria stable IDs and map cross-topic flows to observable outcomes and planned local checks. For a single topic, explicitly mark cross-topic checks not applicable.
3. Record the current work state under `RULES.md`, stage reports/evidence paths, blockers, and next action. Save the plan as `plan.md`, impact assessments as `impact-N.md`, and verification attempts as `verification-N.md` in the same directory. A report may link existing evidence rather than duplicate it.
4. Pin exact approved versions before initial planning. Do not switch them just because a newer draft or approval appears. For adoption, record an explicit target-version mapping in the impact assessment, check target approvals, and re-plan against those targets while old pins remain the execution baseline. Save the revised plan and new pins together in the adoption handoff before resuming implementation. Re-read pinned versions, actual source and open findings when resuming.
5. Set `done` only when code meets acceptance criteria, all required local checks pass, cross-topic checks pass where applicable, and no blocking findings remain. Otherwise record the actual stage or `blocked` with the needed input/action. State that delivery is local.

## Output
Persistent work item with topic/version references, dependencies/order, acceptance/check mapping, current state, evidence and next action.

## Done when
Another run can resume without relying on chat-only state, and the recorded status matches the evidence.

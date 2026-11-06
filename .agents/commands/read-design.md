# read-design

Read the exact design version and approval state needed by a stage.

## Input
Topic(s), work item's pinned versions or explicit requested versions when supplied, `design/index.md`, and the versioned system/topic design paths.

## Gate
A stage needs the current design or must verify approval before planning or implementation.

## Steps
1. For implementation/verification, resolve exact work-item pins. For an explicit design-change re-plan, resolve the approved target-version mapping recorded in the impact assessment without changing execution pins. For analysis, inspect the requested draft/comparison versions separately. Otherwise use explicitly requested versions or the newest approved version. Read matching rows for the topic and, when relevant, `system`; check status, approver, date and decision record against design metadata. A newer draft does not displace an approved version.
2. Read resolved versions and any comparison versions needed to understand a change. Extract business rules, flow, module boundaries, data ownership, contracts, acceptance criteria, open questions, and source references relevant to the task.
3. Report absent files, inconsistent index entries, or a non-approved status when the caller requires approval. Do not infer approval from wording in a document.

## Output
The versions and statuses read, relevant architecture/feature decisions with file references, and any unresolved inconsistency.

## Done when
The caller can identify the exact design version and whether it may be used for the requested stage.

# read-design

Read the exact design version and approval state needed by a stage.

## Input
Topic, `design/index.md`, and the versioned system/topic design paths.

## Gate
A stage needs the current design or must verify approval before planning or implementation.

## Steps
1. Read the index row for the topic and, when relevant, `system`. Check version, status, approver, and date against the referenced files.
2. Read the current version and any older version needed to understand a change. Extract business rules, flow, module boundaries, data ownership, contracts, acceptance criteria, open questions, and source references relevant to the task.
3. Report absent files, inconsistent index entries, or a non-approved status when the caller requires approval. Do not infer approval from wording in a document.

## Output
The versions and statuses read, relevant architecture/feature decisions with file references, and any unresolved inconsistency.

## Done when
The caller can identify the exact design version and whether it may be used for the requested stage.

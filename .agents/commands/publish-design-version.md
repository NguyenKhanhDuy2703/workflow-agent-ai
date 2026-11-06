# publish-design-version

Publish a traceable draft design and update its index entry.

## Input
Topic, original input references, analyzed requirements, relevant flows/rules/interfaces, acceptance criteria, gap report, and `design/index.md` if present.

## Gate
There is enough sourced material to present a meaningful draft. This command publishes draft content; approval is recorded separately by the user or AI through `approve-design-version` under `RULES.md`.

## Steps
1. Use the proposed version reserved during analysis/impact assessment, or choose the next unused `vN` for the topic if none was reserved. An existing draft may be refined at that version; a directory containing only its provisional impact assessment is not an approved design. Never overwrite approved content or revise its original input.
2. Write only relevant design files under `design/docs/<topic>/vN/`. Record source version and `draft` status, then business rules, flow, feature/module boundary, data ownership, contracts, acceptance criteria, missing information, and open questions. For `system`, use `design/docs/system/vN/`.
3. Create the index if absent. Add or update only the row for this topic/version with status `draft`, design path and empty approval fields. Keep other rows intact; a newer draft does not replace an approved version. Supersession follows `RULES.md` and must preserve active work-item pins.
4. Present the draft and questions. Return to the caller for `approve-design-version`; a standalone invocation ends after publication.

## Output
Draft design path, draft index entry, and review questions.

## Done when
The draft is traceable to original input, index and files agree, and no approval or implementation has occurred.

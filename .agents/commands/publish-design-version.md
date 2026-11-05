# publish-design-version

Publish a traceable draft design and update its index entry.

## Input
Topic, original input references, analyzed requirements, relevant flows/rules/interfaces, acceptance criteria, gap report, and `design/index.md` if present.

## Gate
There is enough sourced material to present a meaningful draft. This command publishes **draft only**; approval is reserved for the user under `RULES.md`.

## Steps
1. Choose the next unused `vN` for the topic. Never overwrite an approved version or revise its original input.
2. Write only relevant design files under `design/docs/<topic>/vN/`. Record source version and `draft` status, then business rules, flow, feature/module boundary, data ownership, contracts, acceptance criteria, missing information, and open questions. For `system`, use `design/docs/system/vN/`.
3. Add or update the index entry for this draft with topic, current version, status `draft`, and date; leave approver unset. Keep older approved versions intact. Do not mark an older version `superseded` until the user approves its replacement.
4. Present the draft and questions, then stop the analysis stage.

## Output
Draft design path, draft index entry, and review questions.

## Done when
The draft is traceable to original input, index and files agree, and no approval or implementation has occurred.

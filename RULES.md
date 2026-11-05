# Operating Rules

## Sources and versions

- Treat `design/requirements/` as original input and `design/docs/` as analysis derived from that input. Record the source and version behind each design conclusion.
- Use `design/index.md` to identify the current version and its status. Do not overwrite an approved version; create a new version for a change.
- Do not present assumptions as confirmed requirements, architecture, technology, or implemented modules.

## Topics

- A topic is one user-facing capability or one cross-cutting area, named in kebab-case.
- Reuse an existing topic from `design/index.md` when the request fits it. If a request spans several topics, list them and handle each separately.
- Do not create a new topic without telling the user. If unsure which topic applies, ask.

## Design status

- Status values in `design/index.md`: `draft` → `approved` → `superseded`.
- Each index row records: topic, current version, status, approved by, date.
- The agent may create `draft` versions. Only the user can set `approved`, by explicitly naming the topic and version. The agent must not edit the status to `approved` on its own.
- An older version becomes `superseded` only after the user approves its replacement.

## System design bootstrap

- System design is the reserved topic `system` (`design/docs/system/vN/`).
- If it is missing, the first task is `analyze-design` for `system`, producing a `draft`. No implementation starts until it is `approved`.
- Required input is `design/requirements/system/vN/` or information the user supplies. If neither exists, ask about frontend, backend, database, and build/test tools.

## Missing skills or commands

- If a skill or command file required by `AGENTS.md` does not exist, report it and stop that stage.
- Do not substitute the stage table in `AGENTS.md` as a procedure unless the user explicitly says to proceed that way.

## Missing or conflicting information

- Check documents required by the affected work: system design for implementation; feature requirements for a feature; UI, data, or API design when the task changes that area.
- If required information is missing, report what is missing, why it matters, and the questions needed to continue. Continue independent analysis where possible. Do not implement the dependent part until the information is supplied or the user explicitly decides how to proceed.
- If the request, approved design, and source conflict, show the conflict and obtain a decision before changing the affected part.
- A draft design is not approved. Do not start implementation planning or implementation until the relevant design is `approved` in `design/index.md`.

## Agent authority

- For an authorized task, the agent may inspect files, prepare drafts and plans, edit files within the task's scope, and run relevant checks. Ask before making a decision reserved for the user by these rules.
- Do not merge a branch or push to GitHub unless the user explicitly instructs that specific action. An instruction to implement, test, commit, or finish a task does not authorize merge or push.
- Do not change unrelated files or silently discard existing work.
- Report changed files, checks run and their results, unresolved questions, and any work stopped by these rules.

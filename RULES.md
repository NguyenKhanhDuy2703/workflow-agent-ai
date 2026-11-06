# Operating Rules

## Sources and versions

- Treat `design/requirements/` as original input and `design/docs/` as analysis derived from that input. Record the source and version behind each design conclusion.
- Use `design/index.md` to identify exact versions and their status. Do not overwrite approved design content; create a new version for a design change. Approval metadata may be updated with its decision record.
- Do not present assumptions as confirmed requirements, architecture, technology, or implemented modules.

## Topics

- A topic is one user-facing capability or one cross-cutting area, named in kebab-case.
- Reuse an existing topic from `design/index.md` when the request fits it. Keep each topic's design separate; coordinate requests spanning topics through one work item with explicit dependencies and end-to-end acceptance checks.
- Do not create a new topic without telling the user. If unsure which topic applies, ask.

## Design status

- Status values in `design/index.md`: `draft` → `approved` → `superseded`.
- Keep one index row per topic/version with: topic, version, status, approved by, approval date, decision-record path, and design path. Use ISO dates. A new draft does not replace an approved row. Read the newest approved version by default; active work uses its pinned versions.
- The user or AI may approve an exact topic/version. AI approval requires traceable input, sufficient rules/flows/interfaces and acceptance criteria for the affected scope, no blocking gaps or unresolved requirement conflicts, and a recorded rationale. Record `approved by` as the user identity or `AI (agent identifier)`; never imply that AI approval was user approval.
- Use `.agents/commands/approve-design-version.md` to record approval in both the design metadata and index. AI may approve and continue in the same run without waiting for user confirmation. Honor an explicit user request to review before proceeding.
- AI approval can adopt reasoned technical proposals within the authorized scope; label them as AI decisions, not user-supplied requirements. It cannot invent missing business requirements, override explicit user constraints, or authorize unrelated or external actions.
- Mark an older version `superseded` only after a replacement is approved and no active work item still uses it. Approval of a replacement alone does not switch an active work item to it.

## Project discovery and bootstrap

- Before the first system design, run `.agents/commands/discover-project.md`. Capture goals, users, MVP scope and exclusions, time/budget constraints, data, and target runtime environments before proposing technologies. Reuse discovery on subsequent tasks; update it when these inputs change.
- Preserve original discovery input under `design/requirements/system/discovery/` and derived findings in `design/discovery.md`. Record unknowns explicitly; unspecified deadlines or budgets are not automatically blockers.
- System design is the reserved topic `system` (`design/docs/system/vN/`). If missing, analyze it from discovery and source evidence, then approve it under the rules above before implementation planning.
- For a project without source, include the initial application structure, local configuration and build/test setup in the approved system design and change plan. Do not require existing modules or tests to plan their creation; route only work supported by available skills.

## Work items and local delivery

- For NestJS projects, inspect actual context and use `.agents/references/nestjs/delivery-contracts.md` for design readiness and stage outputs, plus `verification.md` in the same directory for check selection. The primary stack preference does not override an existing approved architecture. Reference conventions are source evidence, not confirmed business policy or permission to upgrade packages.

- A work item is the execution/delivery unit for one request and may link multiple topics. Store it in `work/items/<work-id>/work-item.md`, with its plan, impact assessments, and verification evidence alongside it. Create these records when doing application delivery, not merely when editing workflow procedures.
- Record request/scope, topic/version references including `system`, dependencies and execution order, acceptance criteria including cross-topic flows, required local checks, current stage, blockers, and next action. Pin exact approved versions before planning; store the plan as `plan.md`.
- Work states are `analyzing`, `planned`, `implementing`, `verifying`, `fixing`, `blocked`, and `done`. These are separate from design status. Persist stage handoffs and resume from the record after re-reading the referenced files.
- Before adopting a new design version, record a short impact assessment under the work item: behavior delta, affected topics/contracts/data/files, compatibility and migration impact, rework, invalidated checks, and revised dependencies/order. After replacement approval, re-plan against explicitly recorded target versions while retaining old pins as the execution baseline. Save the revised plan and new pins together in the adoption handoff before implementing the new behavior.
- Completion means code is changed and verified locally against the agreed acceptance criteria, including cross-topic flows. Required local checks must pass and blocking findings must be resolved. A required check that cannot run prevents `done`; optional checks may be recorded as not run with their limits. Do not downgrade required checks merely to finish.
- Local completion does not include push, merge, deployment, or production acceptance. A successful documentation-only task is reported as such, without implying that an application was implemented or tested.

## Verification and repair

- Verification produces evidence and classified findings; the orchestrator routes repairs to the owning implementation skill, then verifies the affected behavior and integration paths again. A standalone verification skill reports the route without starting implementation.
- Classify findings as implementation defects, design changes, or environment blockers. Fix code that contradicts approved behavior against the same version; this does not require a new design or approval. Before switching intended behavior, assess impact, analyze and approve a new design, then re-plan.
- Continue the repair loop while meaningful progress is possible within scope. If a finding recurs after two repair attempts without new evidence or an external dependency prevents progress, record attempts and the next needed input/action, stop dependent retries, and report `blocked`. Continue independent work where possible.

## Missing skills or commands

- If a skill or command file required by `AGENTS.md` does not exist, report it and stop that stage.
- Do not substitute the stage table in `AGENTS.md` as a procedure unless the user explicitly says to proceed that way.

## Missing or conflicting information

- Check documents required by the affected work: system design for implementation; feature requirements for a feature; UI, data, or API design when the task changes that area.
- If required information is missing, report what is missing, why it matters, and the questions needed to continue. Continue independent analysis where possible. Do not implement the dependent part until the information is supplied or the user explicitly decides how to proceed.
- If source contradicts approved behavior, classify whether it is an implementation defect or a proposed design change. Fix clear implementation defects within the authorized scope. If intended behavior is unclear or requirements conflict, show the conflicting sources and obtain the missing user decision before changing the dependent part. AI technical decisions must follow the approval rules above.
- A draft design is not approved. Do not start implementation planning or implementation until the relevant design is `approved` in `design/index.md`.

## Agent authority

- For an authorized task, the agent may inspect files, prepare drafts and plans, approve sufficiently supported designs, edit files within scope, and run relevant local checks. Ask for missing business decisions or actions outside that authority; approval does not expand execution permissions.
- Do not merge a branch or push to GitHub unless the user explicitly instructs that specific action. An instruction to implement, test, commit, or finish a task does not authorize merge or push.
- Do not change unrelated files or silently discard existing work.
- Report changed files, checks run and their results, unresolved questions, and any work stopped by these rules.

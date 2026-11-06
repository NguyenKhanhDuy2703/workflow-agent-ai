# approve-design-version

Evaluate and record user or AI approval of one exact topic/version.

## Input
Draft design and source references, gap report, index if present, any explicit user decision/review request, and an impact assessment when replacing an adopted design.

## Gate
A meaningful draft exists. This command records a decision; it does not implement source or expand the authorized task.

## Steps
1. Check that source-backed goals/rules, flows, boundaries, relevant data/contracts and acceptance criteria sufficiently define the requested scope. Check blocking gaps, requirement conflicts, system compatibility, and cross-topic dependencies. Approval of one topic does not approve its dependencies.
   For NestJS, evaluate every applicable decision in [delivery contracts](../references/nestjs/delivery-contracts.md): operation/owner, route/DTO, access, response/errors, data/invariants, side effects and AC evidence. Record resolved decisions or explicit not-applicable reasons; unknown business policy or a build-only behavior check cannot satisfy this gate.
2. Honor an explicit request for user review. Otherwise AI may approve when these checks pass, documenting why the design is ready and labeling adopted technical proposals as AI decisions. Do not approve through missing business rules or conflicting user constraints. If blocked, retain `draft`, state the missing decision, and continue only independent analysis.
3. Write `approval.md` under the exact design version with the decision, approver (`AI (agent identifier)` or actual user identity), ISO date, source/evidence references, rationale, and non-blocking limitations. For user approval, cite the explicit topic/version decision; never attribute AI approval to the user.
4. Update design approval metadata and the matching index row consistently without changing approved design content. Create the index on first publication if needed. Preserve other version rows. Supersede an older version only when the replacement is approved and no active work item remains pinned to the older version.
5. Report whether planning is now allowed. AI approval may be followed by planning in the same orchestrated run; a standalone invocation ends with this command's report.

## Output
Recorded approval or an explicit blocked decision, consistent design/index metadata, and the next permitted stage.

## Done when
The decision identifies an exact topic/version, its authority and evidence, and approval has not been used to invent requirements or conceal blockers.

---
name: verify-and-review
description: Verify approved acceptance criteria and review local changes, distinguishing NestJS service, module, HTTP and database evidence and routing repair findings.
---

# Verify and review

Verify planned changes and report whether they meet the approved design.

## Core Capabilities

- Run relevant checks and review the diff against acceptance criteria and integration contracts.
- Classify failures and hand repair routes to the orchestrator. This skill does not implement, merge, or push.

For NestJS, use [verification guidance](../../references/nestjs/verification.md) and the [stage handoffs](../../references/nestjs/delivery-contracts.md). Review changed module/provider registration, DTO runtime validation, auth/policy wiring, response/filter behavior, persistence invariants and affected clients. Classify what each check actually exercises; `e2e` filenames and passing builds do not establish HTTP or real-DB coverage.

## Steps

1. Read exact approved versions, the work item when present, acceptance criteria, the change plan, changed files, and local test configuration. Run [run-relevant-tests](../../commands/run-relevant-tests.md), including planned cross-topic flows; record required/optional checks with pass, fail, and not-run results.
2. Run [review-diff](../../commands/review-diff.md) with the diff and test results. Check requirements coverage, unrelated edits, regressions, and contract/migration impact.
3. Run [classify-findings](../../commands/classify-findings.md) and persist evidence in `verification-N.md` when part of a work item. Identify implementation/design/environment routes, repair owners, attempts, and checks to re-run.
4. Run [report-result](../../commands/report-result.md). Include failed or unavailable checks and unresolved findings. Required unavailable checks and blocking defects prevent local completion. The orchestrator returns implementation defects to the owning skill and then invokes verification again; a standalone invocation reports the next route and ends.

## Output and Gate

Report work item when present, topics/versions, changed files, local checks/results including cross-topic acceptance, classified findings, repair routes, blockers, and remaining work. Report local completion only when all required evidence passes and no blocking finding remains.

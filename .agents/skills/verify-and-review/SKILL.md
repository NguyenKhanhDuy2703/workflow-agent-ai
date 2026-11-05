---
name: verify-and-review
description: Verify changes against approved acceptance criteria, review the diff, and report the outcome.
---

# Verify and review

Verify planned changes and report whether they meet the approved design.

## Core Capabilities

- Run relevant checks and review the diff against acceptance criteria and integration contracts.
- Report failures and remaining work. This skill does not implement, merge, or push.

## Steps

1. Read approved acceptance criteria, the change plan, changed files, and test configuration. Run [run-relevant-tests](../../commands/run-relevant-tests.md); record pass, fail, and not-run results.
2. Run [review-diff](../../commands/review-diff.md) with the diff and test results. Check requirements coverage, unrelated edits, regressions, and contract/migration impact.
3. Run [report-result](../../commands/report-result.md). Include failed or unavailable checks and unresolved findings; do not mark work complete with a blocking defect.

## Output and Gate

Report topic/version, changed files, checks and results, review findings, blockers, and remaining work.

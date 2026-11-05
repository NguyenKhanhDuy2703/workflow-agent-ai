# review-diff

Review changed files against the approved plan and design.

## Input
Changed files/diff, approved design and acceptance criteria, change plan, and test results.

## Gate
Before reporting a completed implementation or when reviewing partial work.

## Steps
1. Compare the diff with the planned scope and each relevant acceptance criterion.
2. Inspect module boundaries, data ownership, regressions, unrelated edits, missing tests, contract mismatch, migration impact, and accidental inclusion of sensitive data.
3. Record actionable findings with file and location. Distinguish confirmed defects from uncertainty; do not silently change approved behavior during review.

## Output
Review findings ordered by impact, coverage gaps, and a summary of scope alignment.

## Done when
The implementation can be reported with clear findings and remaining risks.

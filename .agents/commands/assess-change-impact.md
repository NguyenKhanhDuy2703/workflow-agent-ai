# assess-change-impact

Distinguish code corrections from intended design changes and assess impact before adopting a new design.

## Input
Requested change or finding, currently pinned designs, proposed behavior/version, relevant source/contracts/tests, and work item when present.

## Gate
An existing design or implementation is challenged, or work may switch to a different design version. Initial design creation has no previous baseline; record that fact instead of inventing a delta.

## Steps
1. Compare intended behavior with approved rules and observed source. Classify a clear code mismatch as an implementation defect; keep the approved version and route a fix. A change to intended behavior is a design change. If conflicting requirements leave intent unclear, record both sources and ask for the missing decision.
2. For a design change, record the current/proposed versions and behavior delta; affected topics, modules/files, contracts and consumers; data/migration/compatibility effects; work to retain or redo; checks invalidated or added; and dependency/order changes. Note effort or timing impact qualitatively where a reliable estimate is unavailable.
3. Save a short `impact-N.md` under the work item before adopting a replacement. For standalone design analysis with no work item, save `impact.md` under the proposed design version. Initial analysis can be provisional; finalize it against the actual proposed version before approval/adoption.
4. Record an explicit target-version mapping. After replacement approval, pass those targets to re-planning while existing pins remain the execution baseline. Save the revised plan and new pins together in the adoption handoff before implementing the new behavior. Work independent of the change may continue.

## Output
Classification, short impact assessment or a code-only correction rationale, affected acceptance/checks, and repair/design route.

## Done when
The route and consequences are explicit before a version switch, and code-only defects have not been disguised as requirement changes.

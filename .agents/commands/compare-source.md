# compare-source

Map requirements or approved design to current source behavior.

## Input
Topic requirements or approved design, relevant source files, and the task scope.

## Gate
Source exists and analysis or implementation planning needs to know current behavior. Skip with an explicit “no source exists” result for a new project.

## Steps
1. Identify affected modules, their boundaries, integration points, and tests. Note whether calls are internal to a modular monolith or cross separately deployed modules.
2. Compare observable behavior, data movement, and contracts with each relevant requirement/design item. Record matches, gaps, and contradictions with file references.
3. Do not treat existing behavior as an approved requirement. Classify clear code deviations as implementation defects that can be fixed under the same approved design. Route changes to intended behavior through impact assessment and design approval. Escalate unresolved requirement conflicts under `RULES.md` before changing the dependent part.

## Output
A source comparison mapping each relevant requirement to modules, current behavior, integration contracts, and any gap or conflict.

## Done when
The affected source and its relationship to the requested behavior are clear enough for the next stage.

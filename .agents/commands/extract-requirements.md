# extract-requirements

Turn original input into traceable requirements and open questions.

## Input
Original topic input from `design/requirements/<topic>/vN/` or directly from the user, plus the input inventory from `check-input`.

## Gate
Preparing a draft design; never use this command to declare a design approved.

## Steps
1. If the input came directly from the user, preserve a faithful copy under the topic's requirements version before deriving conclusions. Do not rewrite a previously approved input version.
2. Extract in order: business goal and rules; actors and flow; feature boundary; data ownership and movement; contracts and effects on other modules; acceptance criteria. Use ordered steps for a simple flow and flag where a sequence/state diagram is needed.
3. Give each item a source reference. Mark inferred items as proposals and unclear items as questions; do not turn them into confirmed requirements.
4. For NestJS backend tasks, derive the applicable [design decisions](../references/nestjs/delivery-contracts.md) from that input and source: actor/policy, operation and error cases, input/output, persistence invariants and side effects. Give ACs stable IDs with observable outcomes; mark missing business decisions as questions instead of copying reference role/state rules.

## Output
A source-linked requirement list in that order, proposed interpretations, and open questions for design analysis.

## Done when
Every confirmed requirement points to original input, and uncertainty is visible rather than silently filled.

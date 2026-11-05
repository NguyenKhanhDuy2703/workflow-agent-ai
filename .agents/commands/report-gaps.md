# report-gaps

Report missing information, conflicts, and blocked work.

## Input
Input inventory, extracted requirements, source comparison, and current design questions.

## Gate
Analysis finds missing documents, unclear decisions, or conflicts; also run to confirm that no blocking gap remains before publishing a draft.

## Steps
1. Group gaps by missing input, ambiguous requirement, and source/design conflict.
2. For each gap, state the affected topic/version, why it matters, the stage it blocks, and the specific user decision or document needed. For a conflict, name both sources; do not invent a priority between them.
3. Distinguish blocking gaps from non-blocking open questions. Continue only work independent of blocking gaps, as allowed by `RULES.md`.

## Output
A Missing Documents and Open Questions report, or an explicit statement that no gap was found.

## Done when
The user can answer or supply each blocking item without guessing what the agent needs.

# check-input

Inventory topic input and identify missing or conflicting documents.

## Input
Topic, requested work, user-supplied material, `design/index.md` if present, and the relevant requirements/design paths.

## Gate
At the start of analysis or a document-dependent stage. This command inspects inputs only.

## Steps
1. Resolve the topic under `RULES.md`; report a new topic before creating it. Identify the current and proposed versions without overwriting an approved version.
2. Inventory original input, current system/feature design, relevant source, and any UI, data, or API material needed by the requested scope.
3. Mark each item available, missing, or conflicting. Identify whether the project uses a modular monolith, separate services, or both from approved design/source; do not choose an architecture here.

## Output
An input inventory with topic/version, original sources, architecture evidence, missing items, conflicts, and the stages each gap blocks.

## Done when
Every required input has a source or an explicit gap; no missing item has been silently assumed.

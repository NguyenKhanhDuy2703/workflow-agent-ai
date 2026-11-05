---
name: analyze-design
description: Analyze one topic's requirements and relevant source, produce a traceable draft design, and stop for user review.
---

# Analyze design

Analyze one topic and publish a traceable draft. Read `RULES.md`; analyze `system` first if its design is missing.

## Core Capabilities

- Turn original input into business rules, flow, module boundary, data ownership, contracts, and acceptance criteria.
- Expose missing documents and conflicts without inventing decisions. This skill does not plan or implement source changes.

## Steps

1. Run [check-input](../../commands/check-input.md) for the topic, original requirements, and required documents. If no usable source exists, report what is missing and stop.
2. Run [read-design](../../commands/read-design.md) to identify the current versions and decisions to preserve or revise.
3. Run [extract-requirements](../../commands/extract-requirements.md). Organize the draft as **business rules → flow → feature boundary → data ownership → contracts and affected modules**. Use a sequence or state diagram when ordering or transitions need one.
4. Run [compare-source](../../commands/compare-source.md) if source exists; otherwise record that this step was skipped.
5. Run [report-gaps](../../commands/report-gaps.md). Show conflicting sources and ask the user to resolve design conflicts; no conflict priority is defined yet.
6. Run [publish-design-version](../../commands/publish-design-version.md) only when sourced input supports a meaningful draft. It may set `draft`, never `approved`.

## Output and Gate

Report topic/version, draft path, source references, flow, module/data/contract decisions, acceptance criteria, gaps, and open questions. **Stop after presenting the draft.** Planning requires `approved` status in `design/index.md`.

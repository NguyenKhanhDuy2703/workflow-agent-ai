# discover-project

Discover the project context before choosing the system architecture or technologies.

## Input
User request, existing project documents/source, previous discovery if present, and supplied constraints.

## Gate
Before the first system design, or when project goals, scope, constraints, data, or target environments change. Reuse current discovery when these inputs are unchanged.

## Steps
1. Inspect available input before asking questions. Capture business goals and success measures; user groups and their main flows; MVP capabilities and exclusions; deadlines, budget and available capacity; data sources, ownership and sensitivity; and local/target runtime environments and external integrations.
2. Preserve original input without rewriting it under `design/requirements/system/discovery/`. Write source-linked findings in `design/discovery.md`, separating confirmed input, AI proposals, unknowns, and questions. Do not silently turn a technology suggestion into a user requirement.
3. Ask focused questions for unknowns that affect the requested scope or architecture. Mark unspecified time/budget constraints as unspecified rather than inventing numbers or automatically blocking work. Continue analysis independent of blocking questions.
4. Identify inputs ready for system analysis and gaps that prevent it. Do not implement source or declare a system architecture approved in this command.
5. For an existing NestJS target, run or reuse [inspect-nestjs-context](inspect-nestjs-context.md) to attach actual module/bootstrap/access/persistence/test paths and affected consumers to discovery. For a new project, record the NestJS preference and proposed setup separately from confirmed business input; do not claim reference modules already exist.

## Output
Discovery document, original input references, MVP boundary, constraints, data/runtime context, and blocking/non-blocking questions.

## Done when
All discovery areas have sourced findings or explicit unknowns, and the next stage can identify what is supported and what still requires a user decision.

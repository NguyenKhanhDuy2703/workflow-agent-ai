---
name: implement-frontend
description: Implement approved client API mapping, state, and UI changes for a planned topic.
---

# Implement frontend changes

Implement the approved client portion of a fullstack website change.

## Core Capabilities

- Map APIs, wire state, and implement visible behavior in user-facing or admin applications.
- Follow the project's existing client patterns. Backend contracts and data ownership are outside this skill.

When integrating a NestJS API, inspect affected clients separately using the [project profile](../../references/nestjs/project-profile.md). Preserve actual base URL/global prefix, cookie/Bearer credentials, refresh behavior and success/error decoding. A backend-only task does not require UI edits, and learner/admin clients are not assumed to share one implementation.

## Steps

1. Verify the exact design versions referenced by the plan/work item are `approved` in the index. Read user flow, UI states, API contract, and client patterns if present; create initial client files/configuration only as specified by the approved plan. Stop if a required transition or API behavior is undefined. Verification repairs use the same versions unless an assessed design change was approved and re-planned.
2. If API integration changes, run [map-frontend-api](../../commands/map-frontend-api.md).
3. If state or async flow changes, run [wire-frontend-state](../../commands/wire-frontend-state.md) using the API mapping.
4. If visible behavior changes, run [implement-ui](../../commands/implement-ui.md) using the state interface.
5. Run [run-relevant-tests](../../commands/run-relevant-tests.md) for affected client behavior.

## Output and Gate

Report changed files, API/state interfaces, user flows covered, test results, and blockers. Report needed backend changes instead of performing them here.

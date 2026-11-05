---
name: implement-frontend
description: Implement approved client API mapping, state, and UI changes for a planned topic.
---

# Implement frontend changes

Implement the approved client portion of a fullstack website change.

## Core Capabilities

- Map APIs, wire state, and implement visible behavior in user-facing or admin applications.
- Follow the project's existing client patterns. Backend contracts and data ownership are outside this skill.

## Steps

1. Read the approved user flow, UI states, API contract, and current client patterns. Stop if a required transition or API behavior is undefined.
2. If API integration changes, run [map-frontend-api](../../commands/map-frontend-api.md).
3. If state or async flow changes, run [wire-frontend-state](../../commands/wire-frontend-state.md) using the API mapping.
4. If visible behavior changes, run [implement-ui](../../commands/implement-ui.md) using the state interface.
5. Run [run-relevant-tests](../../commands/run-relevant-tests.md) for affected client behavior.

## Output and Gate

Report changed files, API/state interfaces, user flows covered, test results, and blockers. Report needed backend changes instead of performing them here.

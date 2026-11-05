---
name: implement-backend
description: Implement approved backend contract, business logic, and request handling changes for a planned topic.
---

# Implement backend changes

Implement the approved server portion of a fullstack website change.

## Core Capabilities

- Update contracts, business logic, API entrypoints, and planned backend workers.
- Preserve module boundaries and hand off interface changes. UI and AI processing are outside this skill.

## Steps

1. Read the approved business flow, contracts, data handoff, and current backend modules. Stop if an interface, ownership rule, or failure behavior is undefined.
2. If the interface changes, run [update-contract](../../commands/update-contract.md).
3. If business behavior changes, run [implement-service](../../commands/implement-service.md), using the updated contract.
4. If an entrypoint changes, run [implement-controller](../../commands/implement-controller.md), using the contract and service behavior.
5. Run [run-relevant-tests](../../commands/run-relevant-tests.md) for affected backend behavior.

## Output and Gate

Report changed files, endpoints/events, contract consumers, test results, blockers, and the interface other modules must use. Do not cross an approved module boundary directly.

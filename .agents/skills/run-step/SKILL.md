---
name: run-step
description: Run one named request-to-delivery command for a topic when the user asks for a single workflow step.
---

# Run one step

Execute exactly one command from the [command directory](../../commands/).

## Core Capabilities

- Resolve a named command, validate its inputs and gate, and perform it once.
- Report the command's result without advancing to another command or stage.

## Steps

1. Require a `command_id` containing only lowercase letters, digits, and hyphens. Open `.agents/commands/<command_id>.md`; for example, [check-input](../../commands/check-input.md). Stop if the file is missing.
2. Read its Input and Gate sections. Gather the inputs and check `RULES.md` and design status. A direct call does not bypass the `approved` gate.
3. Perform its Steps once and check Done when. Do not invoke the next command automatically.

## Output and Gate

Report topic/version, command ID, input sources, output, changed files, checks, blockers, and next permitted step.

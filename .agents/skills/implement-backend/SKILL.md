---
name: implement-backend
description: Implement planned NestJS backend changes across validated DTOs, access policies, services, controllers, module wiring and local checks; follow actual target conventions.
---

# Implement backend changes

Implement the approved NestJS portion of a fullstack change. Read the [project profile](../../references/nestjs/project-profile.md) and applicable [delivery contracts](../../references/nestjs/delivery-contracts.md). For another established backend stack, preserve its approved design and report profile-specific gaps rather than rewriting it as NestJS.

## Core Capabilities

- Update runtime-validated DTOs/contracts, services, transport/access policy and module/provider wiring, including planned workers.
- Preserve module boundaries and hand off interface changes. UI and AI processing are outside this skill.

## Steps

1. Verify exact plan/work-item design versions are approved. For NestJS, run or reuse [inspect-nestjs-context](../../commands/inspect-nestjs-context.md); for another approved stack, inspect equivalent existing framework/source patterns and report unsupported work without forcing NestJS procedures. Match ACs to planned file/symbol tasks, operation/access policy, data invariants, errors and checks. Missing business behavior blocks its dependent operation; repairs preserve versions unless an assessed replacement was adopted.
2. If an interface changes, run [update-contract](../../commands/update-contract.md) for concrete DTO validation, response/error contracts and consumers. Do not expose persistence fields merely because they exist in Prisma.
3. If a use case changes, run [implement-service](../../commands/implement-service.md) with the approved principal, invariants, transactions and side effects. Reuse actual services/client patterns rather than introducing an unplanned repository/CQRS layer.
4. If transport/access changes, run [implement-controller](../../commands/implement-controller.md). For NestJS connect DTO/pipes, ordered authentication/policy guards, actor identity and response/status behavior; otherwise follow equivalent approved framework handling.
5. For new/changed NestJS providers, modules or config, run [configure-nestjs-module](../../commands/configure-nestjs-module.md). Verify imports/exports, controller/provider registration and parent/root reachability. For other stacks preserve their composition conventions. New-project structure follows the approved system plan.
6. Run [run-relevant-tests](../../commands/run-relevant-tests.md), applying the [verification guidance](../../references/nestjs/verification.md) for NestJS targets. Select service, request-path and composition/DB evidence according to changed behavior and actual framework tooling; do not assume Jest or a lint script.

## Output and Gate

Report AC IDs, exact files/symbols, routes/events and request/response changes, access policy/principal, data/side-effect behavior, module wiring, affected consumers, commands with cwd/results/evidence levels, and blockers. Mark irrelevant areas not applicable. Do not claim HTTP/DB behavior from mocked service checks or cross approved module boundaries directly.

# configure-nestjs-module

Wire approved controllers, providers and configuration into a reachable NestJS module graph.

## Input
Approved module/config decisions, file-level plan, implemented controllers/providers/dependencies, existing graph, and available composition/boot harness.

## Gate
The plan creates a module/provider/controller or changes imports/exports, injection tokens, config or bootstrap. Exact designs must be approved; this command does not choose a new architecture.

## Steps
1. Inspect actual root/owning modules and [delivery contracts](../references/nestjs/delivery-contracts.md). Register controllers/providers in their owner; make new modules reachable through the appropriate parent/root import. Reuse existing providers/tokens.
2. Import the module exporting each cross-module dependency; export only intended interfaces. Respect existing global modules without silently changing scope. Do not duplicate runtime providers, manually construct services in application wiring, or add `forwardRef` to conceal an unresolved cycle. Direct construction in isolated unit tests remains valid but does not prove DI.
3. For approved config changes, update config/validation and non-secret examples where present. Preserve prefix, pipes, auth, filters, cookie/CORS and Swagger unless intentionally changed in approved design. Do not connect to production merely to probe DI.
4. Run or hand off planned build/composition checks through [run-relevant-tests](run-relevant-tests.md). Lifecycle hooks may require isolated resources or controlled overrides; record their limits without overriding the edge under test. Verify reachability, not just compilation.

## Output
Module/config files, provider/import/export map, route reachability and composition evidence or explicit blocker.

## Done when
The intended graph resolves and exposes the behavior, supported by evidence for changed wiring.

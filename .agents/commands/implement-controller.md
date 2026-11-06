# implement-controller

Implement approved API entrypoint behavior.

## Input
Approved API design, change plan, updated contract and service behavior, existing endpoint/handler code, and tests.

## Gate
The plan changes an API entrypoint or its input/output handling. NestJS details below apply to NestJS targets; for another approved framework use its equivalent validation/auth/transport conventions without adding Nest decorators or changing architecture.

## Steps
1. For NestJS, read actual bootstrap/prefix, nearby controller and the approved endpoint/access table in [delivery contracts](../references/nestjs/delivery-contracts.md). Implement the exact method/controller path and status; do not duplicate the global prefix or unintentionally change default POST/DELETE status behavior.
2. Bind concrete body/query/param DTOs and approved conversion/pipes. Apply ID-format validation only when the contract requires it, not merely because example models use UUIDs. Keep runtime validation and Swagger metadata aligned.
3. Wire actual authentication before role/ownership/feature checks as required. Policy decorators and Swagger auth annotations do not enforce access without their guards/registration. Use the validated principal's real identity field for service calls; do not replace it with a body-supplied user ID.
4. Delegate use cases to the service. Preserve existing filters/interceptors, response/error shape and cookie/header behavior. Use raw response objects only where the approved transport needs them, preserving normal Nest response handling where appropriate; do not duplicate business rules.
5. Add/update planned request-path checks for permitted success, validation and applicable authentication/authorization/error cases. Confirm provider/controller wiring through `configure-nestjs-module` when changed; direct controller method calls alone do not prove guards or global pipes ran.

## Output
Changed files/symbols, method/full route/status, DTO/policy/principal wiring, payload/error shape, affected consumers, and endpoint evidence/limits.

## Done when
The endpoint follows the approved contract and delegates the approved behavior to the service.

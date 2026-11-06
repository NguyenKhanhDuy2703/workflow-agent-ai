# update-contract

Update approved API or event contracts and identify consumers.

## Input
Approved API design, change plan, existing shared/API contracts, and known consumers.

## Gate
The plan changes an API request, response, event, or shared type.

## Steps
1. Compare approved method/path/status, request/response or event payload, ownership and flow with current interfaces; identify actual consumers and compatibility impact. For NestJS use applicable [delivery contracts](../references/nestjs/delivery-contracts.md), including the real global prefix, filters/interceptors and client decoding.
2. Update relevant schemas/types/DTO classes in their owning module. For class-validator DTOs, express runtime rules for required/optional/null semantics, bounds/enums, arrays and nested input/conversion when applicable. Use runtime DTO imports for validation; a TypeScript interface or Swagger property alone does not validate payloads. Preserve the target's global ValidationPipe policy.
3. Where Swagger is used, keep metadata/examples aligned with implemented request/status/response behavior and use mapped-type imports compatible with its setup. Do not expose secrets, privilege fields or internal persistence fields unless explicitly intended in the approved interface.
4. Record field deltas, error/status changes, examples, affected learner/admin/service consumers and required checks. If a required field or behavior is undefined, stop that dependent operation and report the missing decision.

## Output
Updated schemas/DTOs and runtime rules, field/status/error delta, payload examples, affected consumers and acceptance checks requiring follow-up.

## Done when
The contract matches approved design, runtime validation and documented metadata agree, and downstream work has an unambiguous interface.

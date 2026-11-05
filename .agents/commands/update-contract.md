# update-contract

Update approved API or event contracts and identify consumers.

## Input
Approved API design, change plan, existing shared/API contracts, and known consumers.

## Gate
The plan changes an API request, response, event, or shared type.

## Steps
1. Compare approved request/response or event payload, ownership, and sync/async flow with current contracts; identify consumers and compatibility impact.
2. Update only the relevant schemas, types, or shared definitions using the project's convention.
3. Record changed fields and required consumer updates. If the approved design leaves a required field or behavior undefined, stop the dependent work and report it.

## Output
Updated contract files, interface changes, and consumers or tests requiring follow-up.

## Done when
The contract matches approved API design and downstream work has an unambiguous interface.

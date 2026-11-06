# map-frontend-api

Map the approved contract into the client API layer.

## Input
Approved UI/flow and API design, change plan, current client API layer, and contract changes.

## Gate
The frontend needs to call or adapt to an API for the planned behavior.

## Steps
1. Locate the established API client or service layer and compare it with the approved backend contract.
   For NestJS integrations, inspect each affected learner/admin client separately using the [project profile](../references/nestjs/project-profile.md): base URL/global prefix, cookie/Bearer credentials, refresh/retry and success/error decoding. Do not invent a shared envelope or copy one client's auth behavior into another without an approved reason.
2. Update request/response or real-time event mapping, including defined errors. Keep network calls in the established client layer.
3. Identify any contract mismatch before wiring state or UI; report undefined API behavior instead of guessing.

## Output
Changed client API mapping, the interface provided to state logic, and any unresolved contract mismatch.

## Done when
Frontend state can consume a clear, contract-aligned interface.

# implement-controller

Implement approved API entrypoint behavior.

## Input
Approved API design, change plan, updated contract and service behavior, existing endpoint/handler code, and tests.

## Gate
The plan changes an API entrypoint or its input/output handling.

## Steps
1. Update the affected controller, route, handler, DTO, validation, or guard according to the project's framework and approved HTTP/event interface.
2. Connect to the service without duplicating business rules in the transport layer.
3. Update endpoint tests for request validation, response shape, and defined failure behavior.

## Output
Changed entrypoint and tests, with the route/event contract passed to consumers.

## Done when
The endpoint follows the approved contract and delegates the approved behavior to the service.

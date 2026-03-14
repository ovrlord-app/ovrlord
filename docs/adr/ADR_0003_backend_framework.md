# ADR 0003 Backend Framework

- Status: Accepted
- Date: 2025-08-15

## Context

Ovrlord requires a backend framework approach that supports API development,
request handling, and middleware composition without adding unnecessary
complexity.

Primary framework requirements are:

- OpenAPI documentation generated from code
- Easy JSON request input and response output handling
- Easy middleware authoring and integration

## Decision

Use **Huma** as the backend API framework.

## Rationale

Huma best matches the project requirements:

- OpenAPI generation from code is a first-class capability
- Strong support for common request/response input and output patterns
- Easy middleware composition
- Built-in support for server-sent events (SSE)

## Alternatives Considered

### No Framework (Go Standard Library Only)

- Excellent for minimizing dependencies
- OpenAPI support is not built in and would require custom implementation or
  additional tooling
- JSON input/output helpers would largely need to be written by the project
- Middleware is fairly straightforward to implement

### Chi

- Popular and feature-rich router/framework approach
- Good ecosystem of third-party middleware
- OpenAPI generation is not provided out of the box

### Gorilla/mux

- Popular and lightweight router with strong routing ergonomics
- OpenAPI generation is not provided out of the box
- Middleware is fairly straightforward to implement

### Huma

- Full OpenAPI generation from code
- Great support for common input/output handling
- SSE support
- Easy to write and integrate

## Consequences

### Positive

- API documentation stays aligned with implementation via code-first generation
- Lower custom boilerplate for JSON request/response handling
- Clear, scalable middleware model for auth, logging, and request lifecycle

### Trade-offs

- Adds framework dependency compared to standard library only
- Team conventions should be documented to ensure consistent Huma usage patterns

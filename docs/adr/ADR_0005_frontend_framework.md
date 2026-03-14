# ADR 0005 Frontend Framework

- Status: Accepted
- Date: 2025-08-15

## Context

Ovrlord needs a frontend framework that supports long-term maintainability and
rapid feature delivery for a rich web UI.

Primary requirements are:

- Strong module ecosystem
- Easy and reliable testing workflows
- Reactive UI development model
- Developer familiarity

## Decision

Use **React** as the frontend framework.

## Rationale

React best satisfies the project priorities:

- Large and mature ecosystem with broad library and tooling availability
- High developer familiarity, reducing onboarding and delivery risk
- Strong component testing patterns and tooling support
- Well-supported workflows with modern tools such as Vite and Vitest for fast,
  browser-independent component testing
- Adequate performance characteristics for the expected UI workload

## Alternatives Considered

### Vue

- Good ecosystem and productive developer experience
- Strong reactivity model
- Fairly easy to test
- Popular, but assessed as less broadly standardized in ecosystem and patterns
  for this team's needs compared to React

### Svelte

- Excellent reactivity and strong performance
- Syntax is closer to native web development in several areas
- Smaller community and module ecosystem than React
- Testing workflows are less straightforward and often require headless browser to test

### React

- Very large ecosystem with varying package quality
- Strong team familiarity
- Decent-to-strong performance for this use case
- Framework-specific syntax and conventions
- Well-established testing patterns and strong support from modern tooling

## Consequences

### Positive

- Faster team ramp-up due to familiarity and established patterns
- Broad package availability for UI, state, routing, and testing needs
- Stable, well-understood testing approach across unit and component layers

### Trade-offs

- Ecosystem breadth requires careful dependency selection and governance
- JSX and React-specific patterns add framework coupling to UI code

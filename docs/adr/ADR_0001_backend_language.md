# ADR 0001 Backend Language

- Status: Accepted
- Date: 2025-08-18

## Context

Ovrlord is a monolithic backend service that must support concurrent workflows such as
indexing, request processing, acquisition orchestration, metadata refresh, and
traceability. The project goals also favor operational simplicity and long-term
maintainability for self-hosted deployments.

The backend language choice should prioritize:

- Safe and practical concurrency support
- Simple packaging and distribution
- Strong out-of-the-box capabilities
- Healthy dependency ecosystem
- Reliable runtime performance
- Team familiarity to reduce delivery risk

## Decision

Use **Go** as the backend implementation language.

## Rationale

Go was selected for the following primary reasons:

1. **Modern concurrency management**
Go's goroutines, channels, and synchronization primitives provide a practical model
for building concurrent backend pipelines without excessive complexity.

2. **Single-binary static compilation**
Go produces standalone binaries that simplify deployment, upgrades, and operations
across self-hosted environments.

3. **Strong standard library**
The standard library provides production-grade building blocks (HTTP, JSON,
context, crypto, testing, etc.), reducing the need for heavy framework dependency.

4. **Mature module ecosystem**
Go modules and the wider ecosystem provide reliable packages for common backend
needs while keeping dependency management straightforward.

5. **Performance characteristics**
Go offers strong runtime performance and efficient resource usage suitable for
always-on backend workloads.

6. **Language familiarity**
Existing familiarity with Go lowers onboarding and delivery risk and enables faster
iteration in early project phases.

## Alternatives Considered

### Node.js

- Highly productive ecosystem, but package quality and conventions are relatively
	fragmented across the module landscape
- Type safety is commonly achieved through TypeScript rather than the language by
	default
- Smaller standard library footprint compared to Go
- Not typically distributed as a single statically linked binary
- Higher memory and CPU overhead was considered a downside for this workload

### Python

- Broad and mature module ecosystem
- Type support is optional and more informal by default
- Common quality gates (formatting, linting, type checking) usually require several
	third-party tools
- Single-binary distribution is possible but generally more complex to achieve
- Performance targets can be met, but often with more tuning and operational
	management

### Elixir

- Excellent concurrency model and strong runtime performance characteristics
- Runs on the Erlang/OTP VM and is not typically packaged as a single static binary
- Smaller talent pool and package ecosystem relative to more mainstream backend
	language options considered for this project

## Consequences

### Positive

- Operationally simple deployments via single executable artifacts
- Fast implementation of concurrent services and background workers
- Lower baseline dependency footprint due to standard library coverage
- Good performance profile for API and worker workloads

### Trade-offs

- Generics and advanced type patterns are less expressive than some alternatives
- Error handling is explicit and can be verbose
- Some domains may require careful package selection due to ecosystem fragmentation

## Notes

This decision establishes the backend language baseline for the project. Framework,
and database decisions are documented in separate ADRs.


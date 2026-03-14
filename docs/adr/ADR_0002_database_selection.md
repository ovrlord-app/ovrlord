# ADR 0002 Database Selection

- Status: Accepted
- Date: 2025-08-15

## Context

Ovrlord needs a primary database for a monolithic backend handling requests,
metadata, acquisition traceability, scheduled jobs, download queue state
tracking, and operational configuration.

The database selection requirements are:

- Open source licensing model
- Support for JSON and modern field types
- Easy setup and operations for self-hosted environments

## Decision

Use **PostgreSQL** as the primary database engine.

## Rationale

PostgreSQL best satisfies the project requirements:

- Fully open source
- Strong performance characteristics for relational workloads
- Advanced JSON/JSONB support and modern data types
- Mature ecosystem and tooling
- Straightforward setup for local and self-hosted deployments
- PostgreSQL 18 includes UUID v7 support, which aligns with modern identifier
  strategies

## Alternatives Considered

### MySQL / MariaDB

- Largely open source, with MariaDB generally viewed as more open than MySQL
- Fairly easy to set up
- Performance and long-term tuning were considered less predictable for this
  project's expected workload compared to PostgreSQL

### MongoDB

- Not aligned with the project's open source preference
- Document model is flexible, but the non-relational approach gives up key
  relational benefits needed for core domain modeling and traceability
- Fairly easy to set up

### Redis Forks

- Extremely fast and simple for cache/queue patterns
- Too limited as the sole primary datastore for the majority of relational
  application use cases in this system
- Would likely drive a multi-database architecture, which is intentionally
  deferred for now
- Fairly easy to set up

### PostgreSQL

- Fully open source
- Fast and reliable for relational workloads
- Strong support for JSON and modern field types
- PostgreSQL 18 adds UUID v7 support
- Fairly easy to set up

### SQLite

- Easiest setup model
- Lower operational complexity for very small deployments
- Lower feature depth and scalability characteristics relative to PostgreSQL for
  this project's needs

## Consequences

### Positive

- Strong relational modeling with modern JSON support in one database
- Good performance without introducing a multi-database architecture early
- Broad compatibility with migration, backup, and operational tooling
- Reliable persistence for scheduler metadata and download queue lifecycle state

### Trade-offs

- Requires running a dedicated database service instead of an embedded file DB
- Operational tuning and maintenance are still required as data volume grows

## Notes

This ADR selects the primary transactional database only. Caching and queueing
technology decisions are deferred to future ADRs if and when needed.

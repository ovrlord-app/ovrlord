# ADR 0004 Database Migration Management

- Status: Accepted
- Date: 2025-08-15

## Context

Ovrlord needs a database migration management approach that is easy to operate,
works well with multiple developers working in parallel, and provides clear
migration state visibility directly from database tracking tables.

Primary requirements are:

- Simple migration workflow
- Supports multiple developers working in tandem without creating migration flow
  conflicts
- Migration tracking table clearly shows which migrations were applied and when
- Preference for native SQL migration files over Go-based migration code

## Decision

Use **goose** for database migration management.

## Rationale

goose best satisfies the project needs:

- Simple and widely adopted migration workflow
- Supports SQL-first migrations while still allowing Go migrations if needed
- Tracks every applied migration in the database, including applied timestamps,
  making migration history easy to audit
- Supports out-of-order migration application, which helps reduce developer
  coordination conflicts in parallel development
- Aligns with a migration-first approach for schema evolution

## Alternatives Considered

### golang-migrate

- Popular and mature migration tool
- Supports SQL-only migrations and a migration-first workflow
- Tracks only the current schema version (last applied migration), which provides
  less granular history visibility than required

### goose

- Popular, simple, and migration-first
- Supports both SQL and Go migrations
- Tracks every applied migration, including apply order and timestamps
- Supports out-of-order application for parallel developer workflows

### Ent (entgo)

- Strong ORM with integrated schema and migration tooling
- Not migration-first in the same way as SQL-file-driven tools
- Introduces ORM-level abstraction and overhead not needed for this project

## Consequences

### Positive

- SQL-first migration authoring aligns with team preference and database-native
  syntax
- Better collaboration for concurrent development due to out-of-order support
- Full migration audit trail available directly from migration tracking tables

### Trade-offs

- Out-of-order migration capability requires discipline in migration naming and
  dependency design
- Team should document migration conventions to avoid semantic conflicts between
  independently authored migrations

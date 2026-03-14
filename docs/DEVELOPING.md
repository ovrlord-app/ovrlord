# Development

## Table of Contents

* [Code Standards](#code-standards)
   * [Tech Stack](#tech-stack)
   * [Frontend](#frontend)
   * [Go](#go)
* [Developing locally](#developing-locally)
   * [Building and running with Docker Compose](#building-and-running-with-docker-compose)
   * [Build and Run without Docker Compose](#build-and-run-without-docker-compose)
   * [Creating SQL Migrations](#creating-sql-migrations)
   * [Format code before commit](#format-code-before-commit)

## Code Standards

### Tech Stack

- **Language**: [Go](https://go.dev/)
- **Database**: [PostgreSQL](https://www.postgresql.org/) with [pgx](https://github.com/jackc/pgx) driver
- **Migrations**: [Goose](https://github.com/pressly/goose)
- **Configuration**: [Viper](https://github.com/spf13/viper)
- **CLI**: [Cobra](https://github.com/spf13/cobra)
- **API Docs Generation**: [Huma](https://huma.rocks/)
- **API UI Client Generation** [Hey-api.ts](https://heyapi.dev/)
- **External APIs**:
   - [TMDB](https://developer.themoviedb.org/) integration

### Frontend

- Follow [Typescript](https://www.typescriptlang.org/) and [React](https://react.dev/) best practices
- Make as much use of [BaseUI](https://base-ui.com/) where possible for ease of Accessibility support.

### Go

- [Code Review Comments guide](https://go.dev/wiki/CodeReviewComments) from the Go project should be
  followed
- [Golangci-lint](https://golangci-lint.run/) with very few configured exceptions

## Developing locally

There are a few ways to run the application locally, the easiest way is to
use [Docker Compose](https://docs.docker.com/compose/), but you can also run
the application directly on your machine provided you have the dependencies installed.

- [Building and running with Docker Compose](#building-and-running-with-docker-compose)
- [Build and Run without Docker Compose](#build-and-run-without-docker-compose)
- [Creating SQL Migrations](#creating-sql-migrations)
- [Format code before commit](#format-code-before-commit)

## Building and running with Docker Compose

```
docker-compose up --build
```

## Build and Run without Docker Compose

### Prerequisites

- [Postgres 18+](https://www.postgresql.org/download/)
- [Go 1.26+](https://golang.org/dl/)
- [Node.js v22+](https://nodejs.org/en/download/)
- [Task](https://taskfile.dev/#/) (recommended) is used to manage development tasks in the project.
- [Goose](https://github.com/pressly/goose) (recommended) is used to manage SQL migrations
- [Caddy Server](https://caddyserver.com/) (optional) is used to run locally with HTTPS

### Install dependencies

With [Task](https://taskfile.dev/#/) running the `task install` command will install dependencies

OR manually run the following commands

```bash
go mod download
cd ui
npm ci
```

#### Build and run

Postgres must be running with the same configuration as in the `docker-compose.yml` file.

With [Task](https://taskfile.dev/#/) run the `task dev` command to build and run the application then visit
[http://localhost:8080](http://localhost:8080) in your browser.

Or `task dev-secure` to run with HTTPS (using Caddy) then
visit [https://ovrlord.localhost](https://ovrlord.localhost) in your browser.

### Format code before commit

- Using the above dev Task(s) will automatically handle this for you.

If you've setup Task simply `task format` to format all go and frontend code before commit.

- not doing so can result in a failed build on GitHub

### Restful API Changes

- Using the above dev Task(s) will automatically handle this for you.

The restful API is documented using OpenAPI comments in the Go code, any changes to that documentation require
regenerating the docs with the following commands and committing the updated docs with the changes.

With [Task](https://taskfile.dev/#/) `task gen-spec` will regenerate the OpenAPI docs

Furthermore, the UI uses a generated api client off the backend generated OpenAPI spec.

### Creating SQL Migrations

Generate new migration file using the following command, replacing `SHORT_DESCRIPTIVE_FILNAME` with a short descriptive
name for the migration example `create_movies_table`.

```
go tool goose -dir internal/db/migrations create SHORT_DESCRIPTIVE_FILNAME sql
```

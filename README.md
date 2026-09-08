# GoCart

GoCart is a **course-based Go backend project** I built while learning practical backend development and concurrency in Go.

The frontend is intentionally simple. The main goal of the project was to practice backend concepts such as authentication, sessions, database access, background work, channels, goroutines, and graceful shutdown.

## Features

- User registration, login, logout, and account activation
- Redis-backed sessions and protected routes
- Subscription plan selection
- Simulated invoice and PDF manual generation
- Background email processing with MailHog
- PostgreSQL data storage
- Docker-based local development
- Tests for routes, handlers, and templates

## Concurrency

Concurrency was one of the main learning areas in the project.

The application uses:

- goroutines for background tasks
- buffered channels for mail processing
- separate error and done channels
- `sync.WaitGroup` to track background work
- `select` inside background listeners
- graceful shutdown with `SIGINT` / `SIGTERM`

After a user subscribes to a plan, invoice and manual-related work can run in the background while email messages are queued through the mail channel.

These flows are intentionally simplified and use dummy data because the project was built for learning rather than as a production payment system.

## Tech Stack

- Go
- Chi
- PostgreSQL
- Redis
- SCS Sessions
- Docker Compose
- MailHog
- Go HTML templates
- goroutines, channels, `sync.WaitGroup`

## Run Locally

Start the supporting services:

```bash
docker compose up -d
```

Set the required environment variables:

```env
DSN=host=localhost port=5433 user=postgres password=password dbname=concurrency sslmode=disable
REDIS=localhost:6379
```

Prepare the database using `db.sql`, then run:

```bash
go run ./cmd/web
```

MailHog UI:

```text
http://localhost:8025
```

## About This Project

I built this project while following a Go course and implementing the application alongside the instructor.

Its main value for me was learning how Go backend concepts fit together in a complete application, especially concurrency, background processing, sessions, middleware, database access, and testing.

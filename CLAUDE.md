# CLAUDE.md

i twp_n8K3U8K1xQYlNIiRjO7SDFgth1as
This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Overview

This is the official [Teamwork.com](https://teamwork.com) MCP (Model Context Protocol) server, written in Go. It exposes Teamwork Projects and Teamwork Desk operations as MCP tools that AI assistants can call. The Go module name is `github.com/teamwork/mcp`.

## Commands

### Development

```bash
# Run servers directly (no build step needed)
go run cmd/mcp-http/main.go        # HTTP server (default :8080)
go run cmd/mcp-stdio/main.go       # STDIO server
go run cmd/mcp-http-cli/main.go    # CLI debugging tool

# Dependencies
go mod tidy
```

### Testing

Tests require live credentials:

```bash
# Run all tests
TWAPI_SERVER=https://yourdomain.teamwork.com/ TWAPI_TOKEN=your_token go test -v ./...

# Run a specific package
go test -v ./internal/twprojects/...

# Run a single test
go test -v -run TestFunctionName ./internal/twprojects/...

# With coverage
go test -v -cover ./...
```

### Linting and Formatting

```bash
golangci-lint -c .golangci.yml run ./...
go fmt ./...
go vet ./...
```

### Docker

```bash
make build        # Build HTTP server Docker image
make build-stdio  # Build STDIO server Docker image
make push         # Push HTTP image to registries
make push-stdio   # Push STDIO image to public registry
```

## Architecture

### Three Entry Points (`cmd/`)

- **`mcp-http`**: Production HTTP server with full middleware stack (auth, logging, DataDog APM, Sentry, body size limits). Used for cloud/hosted deployments.
- **`mcp-stdio`**: STDIO transport for local/desktop integrations. Supports read-only mode.
- **`mcp-http-cli`**: Lightweight CLI tool for testing and debugging.

### Core Internal Packages

**`internal/config/`** — Central configuration and resource wiring. `config.go` creates the HTTP client (optionally with DataDog/HAProxy), initializes the Teamwork API engine, and assembles the MCP server from toolset groups.

**`internal/toolsets/`** — Toolset framework. A `Toolset` groups related read/write tools; a `ToolsetGroup` manages multiple toolsets with enable/disable logic and read-only mode enforcement.

**`internal/twprojects/`** — ~10,000 lines implementing all Teamwork Projects MCP tools (projects, tasks, task lists, users, teams, comments, tags, milestones, timelogs, timers, activities, companies, notebooks, workload, etc.). Each domain file (e.g., `tasks.go`) registers tools via `init()` and exposes a `DefaultToolsetGroup()`.

**`internal/twdesk/`** — Teamwork Desk tools (tickets, messages, users, inboxes, tags, statuses, files), same structure as `twprojects`.

**`internal/auth/`** — Bearer token extraction/validation and bypass logic.

### Adding a New Tool

1. Find or create the relevant domain file under `internal/twprojects/` or `internal/twdesk/`.
2. Register the tool in that file's `init()` function using the toolset framework.
3. Implement the handler using the Teamwork API SDK (`github.com/teamwork/twapi-go-sdk`).
4. Mark it as a read or write tool — write tools are disabled in read-only mode.

### HTTP Middleware Stack (in order)

```
limitBodyMiddleware (10 MB cap)
→ requestInfoMiddleware (trace ID injection)
→ logMiddleware (full req/resp logging)
→ sentryMiddleware (error capture)
→ tracerMiddleware (DataDog APM)
→ authMiddleware (Bearer token validation)
→ Router
```

### Key Environment Variables

| Variable | Purpose | Default |
|---|---|---|
| `TW_MCP_BEARER_TOKEN` | API token for STDIO mode | — |
| `TW_MCP_SERVER_ADDRESS` | HTTP bind address | `:8080` |
| `TW_MCP_LOG_LEVEL` | `debug`/`info`/`warn`/`error` | `info` |
| `TW_MCP_LOG_FORMAT` | `text`/`json` | `text` |
| `TW_MCP_VERSION` | Version string (set at build) | — |

## Documentation

Project docs live in `claude/docs/` (MkDocs). Key references:

- `claude/docs/index.md` — project overview and current status
- `claude/docs/architecture.md` — package map, middleware stack, auth, config wiring
- `claude/docs/tools-reference.md` — full table of MCP tools by domain file
- `claude/docs/workflows.md` — GitHub Issues, Teamwork Tasks, Pull Requests, deploying docs

Serve locally: `./claude/mkdocs-serve.sh` (visit `http://127.0.0.1:8000`)

When starting on an unfamiliar area, read the relevant doc first.

## Code Conventions

- Commit messages follow Conventional Commits: `Chore(deps):`, `Feature:`, `Fix:`, `Chore:`.
- Line length limit: 125 characters (enforced by golangci-lint).
- Cyclomatic complexity limit: 30.
- Linter config: `.golangci.yml` (16 linters enabled including `errcheck`, `staticcheck`, `revive`).
- Tests live alongside source files as `*_test.go`; test helpers in `internal/testutil/`.

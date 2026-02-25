# Architecture

## Package Map

```
cmd/
  mcp-http/       HTTP server (production, cloud)
  mcp-stdio/      STDIO server (local/desktop)
  mcp-http-cli/   CLI debug tool

internal/
  auth/           Bearer token extraction, bypass logic
  config/         Resource wiring: HTTP client, API engine, MCP server assembly
  toolsets/       Toolset + ToolsetGroup framework (enable/disable, read-only mode)
  twprojects/     All Teamwork Projects MCP tools
  twdesk/         All Teamwork Desk MCP tools
  helpers/        Shared utilities
  network/        HTTP logging round-tripper
  request/        HTTP request utilities
  testutil/       Test helpers
```

## HTTP Middleware Stack

Requests through `cmd/mcp-http` pass through this stack in order:

1. `limitBodyMiddleware` — 10 MB cap on request bodies
2. `requestInfoMiddleware` — injects trace ID into context
3. `logMiddleware` — logs full request/response bodies
4. `sentryMiddleware` — captures errors to Sentry
5. `tracerMiddleware` — DataDog APM span creation
6. `authMiddleware` — validates Bearer token or OAuth2 credentials
7. Router — dispatches to MCP handlers

## Toolset Framework (`internal/toolsets/`)

- `Toolset`: a named group of MCP tools (e.g., "tasks", "projects")
- `ToolsetGroup`: owns multiple toolsets; manages enable/disable and read-only enforcement
- Write tools are registered separately and skipped entirely in read-only mode
- `DefaultToolsetGroup()` in each domain package wires up the complete set for that domain

## Tool Registration Pattern

Each domain file (e.g., `internal/twprojects/tasks.go`) uses `init()` to register methods on the toolset. This means adding a blank import of a domain package in a `cmd/` entrypoint is sufficient to activate all its tools.

## Configuration (`internal/config/`)

`config.go` is the main wiring file:
1. Creates the HTTP client (with optional DataDog/HAProxy integration)
2. Initializes the Teamwork API engine (sets base URL, auth headers, middleware)
3. Calls `DefaultToolsetGroup()` on each domain package
4. Assembles the MCP server via `mcp.NewServer()` from the go-sdk

## Authentication

- **HTTP server**: Extracts Bearer token from `Authorization` header; also supports OAuth2 flows. Cross-region requests detected and redirected.
- **STDIO server**: Single static token from `TW_MCP_BEARER_TOKEN` env var.
- **Scopes**: Defined in `internal/config/scopes.go`; checked during auth middleware.

## External Dependencies

| Package | Role |
|---|---|
| `github.com/modelcontextprotocol/go-sdk` | MCP protocol wire format and server |
| `github.com/teamwork/twapi-go-sdk` | Teamwork Projects REST API client |
| `github.com/teamwork/desksdkgo` | Teamwork Desk REST API client |
| `github.com/DataDog/dd-trace-go/v2` | Distributed tracing |
| `github.com/getsentry/sentry-go` | Error reporting |
| `go.opentelemetry.io/*` | OpenTelemetry instrumentation |

# Changelog

## Upstream Merge — March 9, 2026

This page summarizes the 19 commits merged from upstream `main` on 2026-03-09.

---

### New Features

#### Ticket Reply Support (Teamwork Desk)
**Commits:** [#164](https://github.com/Teamwork/mcp/pull/164), [#166](https://github.com/Teamwork/mcp/pull/166)

The `message_create` tool now fully supports replying to Desk tickets.
Previously, the handler was stubbed out with `"not implemented"`.

New parameters on `message_create`:

| Parameter | Type | Description |
|-----------|------|-------------|
| `ticketID` | string | The ticket to reply to (required) |
| `body` | string | Body of the reply (required) |
| `cc` | string[] | Email addresses to CC on the reply |
| `bcc` | string[] | Email addresses to BCC on the reply |

The `create_ticket` tool also gained `cc` and `bcc` array parameters (`internal/twdesk/tickets.go`).

---

#### MCP Apps Extension Enabled
**Commit:** `89e3aa7`

The [MCP Apps Extension](https://github.com/modelcontextprotocol/ext-apps/blob/main/specification/2026-01-26/apps.mdx) is now enabled in the server configuration (`internal/config/config.go`). This allows MCP clients that support the Apps extension to take advantage of richer app-level capabilities.

---

#### Web Linker in Metadata
**Commit:** `e37fb73`

MCP tool responses now include a `webLinker` field in the `meta` section. This provides direct web-app URLs for items returned by the server (tasks, projects, users, tickets, etc.), enabling clients to link users back to the Teamwork web interface.

Affected domains: activities, comments, companies, industries, job roles, milestones, notebooks, project categories, projects, skills, tags, task lists, tasks, teams, timelogs, timers, tickets, users.

New helpers:
- `internal/helpers/schema_meta.go` — `webLinker` schema and structured representation
- `internal/helpers/web_linker.go` — URL construction logic

---

### Enhancements

#### Flexible Number Parsing (Postel's Law)
**Commit:** `22a501f`

Tool parameter parsing now accepts stringified numbers (e.g. `"42"`) wherever a numeric value is expected. This improves compatibility with clients that send numbers as JSON strings.

> *"Be flexible in what you accept and strict in what you send."* — Postel's Law

Implemented in `internal/helpers/tool_parser.go`.

---

#### Improved Required Date Error Messages
**Commit:** `12ec9d1`

When a required date parameter is missing or empty, the error message is now human-readable:

```
Before: invalid parameters: error binding parameter: invalid date format for date:
        parsing time "" as "2006-01-02": cannot parse "" as "2006"

After:  invalid parameters: error binding parameter: parameter date is required
        and cannot be empty
```

Implemented in `internal/helpers/tool_parser.go`.

---

### Bug Fixes

| Commit | Description |
|--------|-------------|
| `e37fb73` | Fix: `webLinker` was missing from metadata output schema and structured response |
| `cb64f5b` | Fix: Disable DNS localhost protection for dev environments (related to [go-sdk #760](https://github.com/modelcontextprotocol/go-sdk/pull/760)) |

---

### Dependency Updates

| Package / Action | Old Version | New Version |
|-----------------|-------------|-------------|
| `github.com/getsentry/sentry-go` | 0.42.0 | 0.43.0 |
| `github.com/getsentry/sentry-go/slog` | — | bumped |
| `go.opentelemetry.io/otel/sdk` | 1.38.0 | 1.40.0 |
| `github.com/modelcontextprotocol/go-sdk` | — | bumped |
| `docker/login-action` (CI) | 3 | 4 |
| `docker/setup-buildx-action` (CI) | 3 | 4 |
| `actions/upload-artifact` (CI) | 6 | 7 |
| `actions/download-artifact` (CI) | 7 | 8 |
| `hono` (Node.js examples) | — | bumped |
| `@hono/node-server` (Node.js examples) | — | bumped |
| `express-rate-limit` (Node.js examples) | — | bumped |

---

### Other

- **README:** Added [Go Report Card](https://goreportcard.com/report/github.com/Teamwork/mcp) badge (#170).

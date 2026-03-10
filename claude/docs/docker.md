# Docker & Local Development

The project ships a multi-stage `Dockerfile` and a `Makefile` that cover building,
running, and deploying the server without needing Go installed locally.

---

## Prerequisites

- [Docker](https://docs.docker.com/get-docker/) with BuildKit / `docker buildx`
- A Teamwork API token

---

## Docker Compose — `docker compose up -d`

The project includes `local.yml` as its Compose file. TAG's dev environment already has
`export COMPOSE_FILE=local.yml` in `~/.zshrc`, so the standard command just works:

```bash
docker compose up -d
```

To rebuild the image after code changes:

```bash
docker compose up -d --build
```

To tail logs:

```bash
docker compose logs -f
```

To stop:

```bash
docker compose down
```

### Environment variables

Copy `.env.example` to `.env` and adjust as needed:

```bash
cp .env.example .env
```

The Compose-relevant variables (with defaults):

| Variable | Default | Description |
|----------|---------|-------------|
| `TW_MCP_PORT` | `8080` | Host port the server is exposed on |
| `TW_MCP_LOG_LEVEL` | `info` | `debug` / `info` / `warn` / `error` |
| `TW_MCP_LOG_FORMAT` | `text` | `text` or `json` |

### Connecting an MCP client

Once running, point your MCP client at:

```
http://localhost:8080
```

Pass your Teamwork API token as the Bearer token in each request:

```
Authorization: Bearer <your_teamwork_api_token>
```

The server forwards that token to the Teamwork API — no separate server credential needed.

---

## Quick Start — compile check

If you just want to verify the Go code compiles (e.g. after making local changes without
Go installed), build only the builder stage:

```bash
docker build --target builder -t mcp-build-check .
```

Any compile errors will surface in the Docker output. A clean exit means the code is good.

---

## Building Images

### HTTP server (default)

```bash
make build
```

Equivalent to:

```bash
docker buildx build \
  --build-arg BUILD_DATE=$(date -u +'%Y-%m-%dT%H:%M:%SZ') \
  --build-arg BUILD_VCS_REF=$(git rev-parse --short HEAD) \
  --build-arg BUILD_VERSION=dev \
  --load \
  --progress=plain \
  --target runner \
  .
```

### STDIO server

```bash
make build-stdio
```

Builds the full image (both binaries are compiled), but the entrypoint is `/bin/tw-mcp-stdio`.

---

## Running Locally

### HTTP server

```bash
docker run --rm \
  -e TW_MCP_BEARER_TOKEN=your_token \
  -p 8080:8080 \
  mcp-build-check
```

The server listens on `:8080`. MCP clients connect with:

```
Authorization: Bearer your_token
```

### STDIO server

```bash
docker run --rm -i \
  -e TW_MCP_BEARER_TOKEN=your_token \
  --entrypoint /bin/tw-mcp-stdio \
  mcp-build-check
```

Pass `--read-only` flag (via `TW_MCP_READ_ONLY=true` or the binary flag) to disable all
write tools.

---

## Dockerfile Structure

The `Dockerfile` uses three stages:

| Stage | Base image | Purpose |
|-------|-----------|---------|
| `builder` | `golang:1.26-alpine` | Downloads deps, compiles both binaries |
| `runner` | `alpine:3` | Minimal runtime image, HTTP entrypoint |
| `stdio` | `runner` | Same image, STDIO entrypoint |

Both binaries (`tw-mcp-http`, `tw-mcp-stdio`) are compiled in the builder stage and copied
into the runner. The final image contains no Go toolchain.

---

## Environment Variables

| Variable | Purpose | Default |
|----------|---------|---------|
| `TW_MCP_BEARER_TOKEN` | Auth token clients must supply | — |
| `TW_MCP_SERVER_ADDRESS` | HTTP bind address | `:8080` |
| `TW_MCP_LOG_LEVEL` | `debug` / `info` / `warn` / `error` | `info` |
| `TW_MCP_LOG_FORMAT` | `text` / `json` | `text` |
| `TW_MCP_VERSION` | Version string (set at build via `BUILD_VERSION` arg) | — |

---

## Pushing to Registries

### Public (GitHub Container Registry)

```bash
make push-stdio
```

Tags: `ghcr.io/teamwork/mcp:vX.Y.Z` and `ghcr.io/teamwork/mcp:latest`.

### Internal (AWS ECR)

```bash
make push
```

Tags against the internal ECR registry using the current branch name.

---

## Tips

**Iterating without rebuilding the whole image** — use a bind mount against the builder stage
during development:

```bash
docker run --rm \
  -v $(pwd):/usr/src/mcp \
  -w /usr/src/mcp \
  golang:1.26-alpine \
  go build ./...
```

This gives you a fast compile loop using the same Go version as the Dockerfile, without
installing Go on your host machine.

**Watching logs in JSON mode:**

```bash
docker run --rm \
  -e TW_MCP_BEARER_TOKEN=your_token \
  -e TW_MCP_LOG_FORMAT=json \
  -p 8080:8080 \
  mcp-build-check | jq .
```

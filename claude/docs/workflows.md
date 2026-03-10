# Workflows

There are several ways to run the Teamwork MCP server depending on your setup. Docker Compose is the recommended starting point since it requires no local toolchain. The sections below cover each option, followed by LangChain integration for Node and Python.

## Run Options

| Method | Requires | Best for |
|--------|----------|---------|
| [Docker Compose](#docker-compose) | Docker | Most developers — no Go needed |
| [Docker (manual)](#docker-manual) | Docker | Custom image tags, CI/CD |
| [Go directly](#go-directly) | Go 1.26+ | Active development on the server itself |
| [Public hosted](#public-hosted-server) | Nothing | Quick client testing |

---

## Docker Compose

The recommended way to run the server locally. See [Docker & Local Dev](docker.md) for full details.

```bash
cp .env.example .env   # first time only
docker compose up -d
```

The server starts on `http://localhost:8787`. Rebuild after code changes:

```bash
docker compose up -d --build
```

---

## Docker (manual)

### Using the public image

The public image at `ghcr.io/teamwork/mcp:latest` runs the **STDIO server**:

```bash
docker run --rm -i \
  -e TW_MCP_BEARER_TOKEN=$TEAMWORK_API_KEY \
  ghcr.io/teamwork/mcp:latest
```

### Building locally

```bash
make build        # HTTP server image (--target runner)
make build-stdio  # STDIO server image
```

Run the locally built HTTP server:

```bash
docker run --rm -p 8787:8080 \
  -e TW_MCP_LOG_LEVEL=debug \
  <image-id>
```

### Build targets

| Target | Entrypoint | Use case |
|--------|-----------|---------|
| `runner` (`make build`) | `tw-mcp-http` | HTTP server, cloud deployments |
| `stdio` (`make build-stdio`) | `tw-mcp-stdio` | Desktop/local STDIO clients |

Both binaries are present in both images — only the entrypoint differs.

---

## Go Directly

Requires Go 1.26+ installed locally. No build step needed — `go run` compiles on the fly.

```bash
# HTTP server — binds :8080
go run cmd/mcp-http/main.go

# STDIO server
TW_MCP_BEARER_TOKEN=$TEAMWORK_API_KEY go run cmd/mcp-stdio/main.go

# STDIO with read-only mode
TW_MCP_BEARER_TOKEN=$TEAMWORK_API_KEY go run cmd/mcp-stdio/main.go -read-only

# STDIO with specific toolsets only
TW_MCP_BEARER_TOKEN=$TEAMWORK_API_KEY go run cmd/mcp-stdio/main.go \
  -toolsets=twprojects-list_projects,twprojects-get_project,twprojects-list_tasks
```

### Connecting a STDIO client

Add this to your MCP client config (e.g. `~/Library/Application Support/Claude/claude_desktop_config.json`):

```json
{
  "mcpServers": {
    "teamwork": {
      "command": "go",
      "args": ["run", "/path/to/teamwork-mcp/cmd/mcp-stdio/main.go"],
      "env": {
        "TW_MCP_BEARER_TOKEN": "your-bearer-token"
      }
    }
  }
}
```

---

## Public Hosted Server

Teamwork operates a hosted MCP endpoint at `https://mcp.ai.teamwork.com`. Useful for testing clients without running anything locally.

---

## Node (LangChain)

An interactive CLI that connects to the MCP server and forwards your prompts to an LLM via LangChain. Located in `examples/nodejs-langchain/`. Use this when you're building a custom application that needs to orchestrate an LLM with Teamwork tools — not for everyday interactive use.

### Setup

```bash
cd examples/nodejs-langchain
npm install
npm run build       # compiles TypeScript → dist/
```

### Run

```bash
npm start -- \
  --bearer-token TEAMWORK_API_KEY \
  --llm-model openai:gpt-4o-mini \
  --server-url https://mcp.ai.teamwork.com
```

Or set the token via environment variable:

```bash
export TW_MCP_BEARER_TOKEN=$TEAMWORK_API_KEY
npm start -- --llm-model anthropic:claude-sonnet-4-6
```

Type `exit` at the `tw-client>` prompt to quit.

### Options

| Flag | Default | Description |
|------|---------|-------------|
| `-t, --bearer-token` | `$TW_MCP_BEARER_TOKEN` | API token |
| `-m, --llm-model` | `openai:gpt-4o-mini` | `provider:model` |
| `-s, --server-url` | `https://mcp.ai.teamwork.com` | MCP server URL |

### Supported providers

| Provider prefix | Models |
|----------------|--------|
| `openai` | `gpt-4o`, `gpt-4o-mini`, etc. |
| `anthropic` | `claude-sonnet-4-6`, `claude-opus-4-6`, etc. |
| `google_genai` | `gemini-2.0-flash`, etc. |

Requires the corresponding API key in the environment (`OPENAI_API_KEY`, `ANTHROPIC_API_KEY`, `GOOGLE_API_KEY`).

---

## Python (LangChain)

Same concept as the Node example, in Python. Located in `examples/python-langchain/`.

### Setup

```bash
cd examples/python-langchain
pip install -r requirements.txt
```

### Run

```bash
python main.py \
  --bearer-token TEAMWORK_API_KEY \
  --llm-model openai:gpt-4.1 \
  --server https://mcp.ai.teamwork.com
```

Or via environment variable:

```bash
export TW_MCP_BEARER_TOKEN=$TEAMWORK_API_KEY
python main.py --llm-model anthropic:claude-sonnet-4-6
```

Type `exit` at the `tw-client>` prompt to quit (or Ctrl+C).

### Options

| Flag | Default | Description |
|------|---------|-------------|
| `--bearer-token` | `$TW_MCP_BEARER_TOKEN` | API token |
| `--llm-model` | `openai:gpt-4.1` | `provider:model` |
| `--server` | `https://mcp.ai.teamwork.com` | MCP server URL |

### Supported providers

| Provider prefix | Package |
|----------------|---------|
| `openai` | `langchain-openai` |
| `anthropic` | `langchain-anthropic` |
| `google_genai` | `langchain-google-genai` |

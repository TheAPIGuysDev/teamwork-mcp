# Workflows

The simplest way to get started is with the [Quick Start method](#quick-start). For integrating with an LLM framework, jump to the [Node](#node-langchain) or [Python](#python-langchain) sections.

## Quick Start

Run the server directly with Go — no build step required.

```bash
# STDIO mode (desktop/local — Claude Desktop, VS Code, etc.)
TW_MCP_BEARER_TOKEN=your_token go run cmd/mcp-stdio/main.go

# STDIO with read-only mode
TW_MCP_BEARER_TOKEN=your_token go run cmd/mcp-stdio/main.go -read-only

# STDIO with specific toolsets only
TW_MCP_BEARER_TOKEN=your_token go run cmd/mcp-stdio/main.go \
  -toolsets=twprojects-list_projects,twprojects-get_project,twprojects-list_tasks

# HTTP mode (production — binds :8080 by default)
go run cmd/mcp-http/main.go
```

### Connecting a client (STDIO)

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

## Docker

### Using the public image

The public image at `ghcr.io/teamwork/mcp:latest` runs the **STDIO server**:

```bash
docker run --rm -i \
  -e TW_MCP_BEARER_TOKEN=your_token \
  ghcr.io/teamwork/mcp:latest
```

### Building locally

```bash
make build        # builds HTTP server image (--target runner)
make build-stdio  # builds STDIO server image (default target)
```

Run the locally built HTTP server:

```bash
docker run --rm -p 8080:8080 \
  -e TW_MCP_LOG_LEVEL=debug \
  <image-id>
```

### Build targets

| Target | Entrypoint | Use case |
|---|---|---|
| `runner` (`make build`) | `tw-mcp-http` | HTTP server, cloud deployments |
| `stdio` (`make build-stdio`) | `tw-mcp-stdio` | Desktop/local STDIO clients |

Both binaries are present in both images — only the entrypoint differs.

---

## Node (LangChain)

An interactive CLI that connects to the MCP server and forwards your prompts to an LLM via LangChain. Located in `examples/nodejs-langchain/`.

### Setup

```bash
cd examples/nodejs-langchain
npm install
npm run build       # compiles TypeScript → dist/
```

### Run

```bash
npm start -- \
  --bearer-token your_token \
  --llm-model openai:gpt-4o-mini \
  --server-url https://mcp.ai.teamwork.com
```

Or set the token via environment variable:

```bash
export TW_MCP_BEARER_TOKEN=your_token
npm start -- --llm-model anthropic:claude-sonnet-4-6
```

Type `exit` at the `tw-client>` prompt to quit.

### Options

| Flag | Default | Description |
|---|---|---|
| `-t, --bearer-token` | `$TW_MCP_BEARER_TOKEN` | API token |
| `-m, --llm-model` | `openai:gpt-4o-mini` | `provider:model` |
| `-s, --server-url` | `https://mcp.ai.teamwork.com` | MCP server URL |

### Supported providers

| Provider prefix | Models |
|---|---|
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
  --bearer-token your_token \
  --llm-model openai:gpt-4.1 \
  --server https://mcp.ai.teamwork.com
```

Or via environment variable:

```bash
export TW_MCP_BEARER_TOKEN=your_token
python main.py --llm-model anthropic:claude-sonnet-4-6
```

Type `exit` at the `tw-client>` prompt to quit (or Ctrl+C).

### Options

| Flag | Default | Description |
|---|---|---|
| `--bearer-token` | `$TW_MCP_BEARER_TOKEN` | API token |
| `--llm-model` | `openai:gpt-4.1` | `provider:model` |
| `--server` | `https://mcp.ai.teamwork.com` | MCP server URL |

### Supported providers

| Provider prefix | Package |
|---|---|
| `openai` | `langchain-openai` |
| `anthropic` | `langchain-anthropic` |
| `google_genai` | `langchain-google-genai` |

# Using the Teamwork MCP Server

!!! warning "This is a local Docker installation — not the public Teamwork server"
    You are running **our fork** of the Teamwork MCP server inside Docker on your own machine.
    This is not the public `mcp.ai.teamwork.com` endpoint.

    This fork adds features not yet in upstream — most notably **date-based task filtering**
    (`today`, `overdue`, `this week`, custom date ranges). The server runs entirely on your
    machine; your Teamwork API token never passes through any third-party service.

---

## What is this server?

The Teamwork MCP Server is a bridge between an AI assistant (like Claude) and your Teamwork
account. Once connected, you can ask the AI plain-English questions and it will look up real
data from your Teamwork projects, tasks, and tickets on your behalf.

**Examples of what you can ask:**

- "What tasks are due today?"
- "Show me all overdue tasks assigned to me"
- "What tasks are due this week in the Website Redesign project?"
- "Create a task called 'Review proposal' in the Marketing project"
- "List all open tickets in the support inbox"

The AI translates your question into an API call, runs it, and returns the results in plain
language. You never need to touch the API directly.

---

## Before you start

You need two things:

1. **The server running locally** — see [Docker & Local Dev](docker.md) to start it with
   `docker compose up -d`. Once running, visit `http://localhost:8787` in your browser
   to confirm it shows the server welcome page.

2. **Your Teamwork API token** — find this in your Teamwork account under
   *Your Profile → API Keys*. It looks like `twp_xxxxxxxxxxxx`.

---

!!! note "Each client has its own config file"
    These are separate applications with separate config files. Connecting one does **not**
    connect the other. Set up each client you want to use independently.

    | Client | Config location |
    |--------|----------------|
    | Claude Desktop | `~/Library/Application Support/Claude/claude_desktop_config.json` |
    | Claude Code (CLI) | `~/.claude.json` (written by `claude mcp add`) |
    | VS Code / Cursor | MCP settings panel inside the app |

---

## Connecting to Claude Desktop

Claude Desktop is the most common way to use this server interactively.

1. Open the Claude Desktop config file:
   - **Mac:** `~/Library/Application Support/Claude/claude_desktop_config.json`
   - **Windows:** `%APPDATA%\Claude\claude_desktop_config.json`

2. Add this entry (replace `TEAMWORK_API_KEY` with your token from `.env`):

```json
{
  "mcpServers": {
    "teamwork-local": {
      "type": "http",
      "url": "http://localhost:8787",
      "headers": {
        "Authorization": "Bearer TEAMWORK_API_KEY"
      }
    }
  }
}
```

3. Restart Claude Desktop. You should see "teamwork-local" listed under connected tools.

4. Start a new conversation and ask: *"What tasks are due today?"*

---
## What to do if not Connected

If you check for your MCP servers and you see an error like the one above, the most likely
cause is that the local Docker server is not running or is unreachable.

**Step 1 — Confirm the server is running:**

```bash
docker compose ps
```

The `teamwork-mcp` container should show `running`. If it shows `exited` or is missing:

```bash
docker compose up -d
```

Then visit `http://localhost:8787` in your browser. You should see the server welcome page.
If you see "Connection refused", the container did not start — check logs with:

```bash
docker compose logs teamwork-mcp
```

**Step 2 — Re-check your client config:**

Make sure the URL and token in your client config exactly match your `.env`:

- URL: `http://localhost:8787` (or whatever `TW_MCP_PORT` is set to)
- Header: `Authorization: Bearer twp_xxxxxxxxxxxx`

**Step 3 — Restart your AI client:**

Claude Desktop and VS Code need a full restart after config changes — closing and reopening
the window is not always enough. Quit the app completely and relaunch it.

**Step 4 — Re-run the `claude mcp add` command (Claude Code only):**

If the server URL or token changed, remove the old entry and re-add it:

```bash
claude mcp remove teamwork-local
claude mcp add teamwork-local --transport http http://localhost:8787 \
  --header "Authorization: Bearer TEAMWORK_API_KEY"
```

---

## Connecting to Claude Code (terminal)

Run this once from your terminal:

```bash
claude mcp add teamwork-local --transport http http://localhost:8787 \
  --header "Authorization: Bearer TEAMWORK_API_KEY"
```

Then type `/mcp` to verify the connection is active.

---

## Connecting to VS Code Copilot or Cursor

Add the server URL and Bearer token in your MCP settings panel. The exact location varies by
tool — look for **MCP Servers** or **Tool Connections** in the settings.

---

## What can I ask?

| What you want | What to ask |
|---------------|-------------|
| Tasks due today | "What tasks are due today?" |
| Overdue tasks | "Show me all overdue tasks" |
| This week's tasks | "What's on my plate this week?" |
| Tasks within 7 days | "What tasks are due in the next 7 days?" |
| Tasks by project | "List tasks in the [Project Name] project" |
| Create a task | "Create a task called '[Name]' in [Project] due [Date]" |
| Update a task | "Mark task [ID] as complete" |
| Support tickets | "Show me open tickets in the support inbox" |
| Reply to a ticket | "Reply to ticket [ID] saying [message]" |

---

## Checking the server is healthy

Visit `http://localhost:8787/api/health` — it should return `OK`.

Opening `http://localhost:8787` directly will show the server welcome page confirming it is
running. The MCP endpoint itself requires a valid Teamwork API token, which your AI client
supplies automatically once configured.

---

## Troubleshooting

**"I don't see any results"**
Make sure the server is running (`docker compose ps`) and your API token is correct.

**"Connection refused"**
The container may not be running. Run `docker compose up -d` from the project folder.

**"Unauthorized" when the AI tries to fetch data**
Your API token is missing or expired. Get a fresh one from your Teamwork profile and update
the token in your AI client config.

**The container stopped after a restart**
`local.yml` uses `restart: unless-stopped` so it should auto-start with Docker. If not, run
`docker compose up -d` again.

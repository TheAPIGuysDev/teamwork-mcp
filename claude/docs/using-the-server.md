# Using the Teamwork MCP Server

This guide is for anyone who wants to use the server with an AI assistant —
no technical background required.

---

## What is this server?

The Teamwork MCP Server is a bridge between an AI assistant (like Claude) and your
Teamwork account. Once connected, you can ask the AI plain-English questions and it will
look up real data from your Teamwork projects, tasks, and tickets on your behalf.

**Examples of what you can ask:**

- "What tasks are due today?"
- "Show me all overdue tasks assigned to me"
- "Create a task called 'Review proposal' in the Marketing project"
- "List all open tickets in the support inbox"
- "What tasks are due this week in the Website Redesign project?"

The AI translates your question into an API call, runs it, and returns the results in
plain language. You never need to touch the API directly.

---

## Before you start

You need two things:

1. **The server running** — see [Docker & Local Dev](docker.md) to start it with
   `docker compose up -d`. Once running, visit `http://localhost:8787` in your browser
   to confirm it says "Running".

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

2. Add this entry (replace `TEAMWORK_API_KEY` with the value from your `.env`):

```json
{
  "mcpServers": {
    "teamwork": {
      "type": "http",
      "url": "http://localhost:8787",
      "headers": {
        "Authorization": "Bearer TEAMWORK_API_KEY"
      }
    }
  }
}
```

3. Restart Claude Desktop. You should see "teamwork" listed under connected tools.

4. Start a new conversation and ask something like: *"What tasks are due today?"*

---

## Connecting to Claude Code (terminal)

If you use Claude Code in the terminal, run this once:

```bash
claude mcp add teamwork --transport http http://localhost:8787 \
  --header "Authorization: Bearer TEAMWORK_API_KEY"
```

Then type `/mcp` to verify the connection is active.

---

## Connecting to VS Code Copilot or Cursor

Add the same server URL and Bearer token in your MCP settings panel. The exact location
varies by tool — look for "MCP Servers" or "Tool Connections" in the settings.

---

## What can I ask?

Here are some ready-to-use prompts to get started:

| What you want | What to ask |
|---------------|-------------|
| Tasks due today | "What tasks are due today?" |
| Overdue tasks | "Show me all overdue tasks" |
| This week's tasks | "What's on my plate this week?" |
| Tasks by project | "List tasks in the [Project Name] project" |
| Create a task | "Create a task called '[Name]' in [Project] due [Date]" |
| Update a task | "Mark task [ID] as complete" |
| Support tickets | "Show me open tickets in the support inbox" |
| Reply to a ticket | "Reply to ticket [ID] saying [message]" |

---

## Checking the server is healthy

Visit `http://localhost:8787/api/health` in your browser. It should return `OK`.

If you see `Unauthorized` on the main page at `http://localhost:8787`, that is normal — the
welcome page should load fine, but the MCP endpoint itself requires a valid Teamwork API token
which your AI client provides automatically once configured.

---

## Troubleshooting

**"I don't see any results"**
Make sure the server is running (`docker compose ps`) and your API token is correct.

**"Connection refused"**
The container may not be running. Run `docker compose up -d` from the project folder.

**"Unauthorized" when the AI tries to fetch data**
Your API token is missing or expired. Get a fresh one from your Teamwork profile and
update the token in your AI client config.

**The container stopped after a restart**
`local.yml` uses `restart: unless-stopped` so it should auto-start with Docker.
If not, run `docker compose up -d` again.

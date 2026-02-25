# TAG Workflow

As with many TAG repos, you can interface with other tools by creating a `.env` with your access credentials. You do things like:

- [Create a Github Issue](#creating-a-github-issue)
- [Create a Github Pull Request](#creating-a-pull-request)
- [Create a Teamwor Task](#creating-a-teamwork-task)
- [Running MkDocs Locally](#serve-locally-first)
- [Push MkDocs to Server](#pushing-docs-to-the-server)

## Creating a GitHub Issue

Use GitHub Issues to track bugs, feature requests, and questions.

```bash
# Bug report
gh issue create \
  --title "Fix: brief description of the problem" \
  --body "## What happened

## Expected behavior

## Steps to reproduce

## Environment (Go version, OS)" \
  --label bug

# Feature request
gh issue create \
  --title "Feature: brief description" \
  --body "## Use case

## Proposed solution

## Alternatives considered" \
  --label enhancement
```

Or open interactively: `gh issue create`

Browse issues: `gh issue list` / `gh issue view <number>`

---

## Creating a Teamwork Task

Use Teamwork tasks to track development work linked to client-facing project management.

Key IDs (from `.env`):

| Variable | Purpose |
|---|---|
| `TEAMWORK_PROJECT_ID` | Main project |
| `TEAMWORK_TASKLIST_ID` | Default task list |
| `TEAMWORK_PARENTTASK_ID` | Parent task for subtasks |

```bash
# Create a task via curl (uses .env values)
source .env

curl -s -X POST \
  "https://${TEAMWORK_WORKSPACE_URL}/projects/${TEAMWORK_PROJECT_ID}/tasks.json" \
  -H "Authorization: Bearer ${TEAMWORK_API_KEY}" \
  -H "Content-Type: application/json" \
  -d '{
    "todo-item": {
      "content": "Task title",
      "description": "Details here",
      "tasklistId": '"${TEAMWORK_TASKLIST_ID}"'
    }
  }'
```

Or use the MCP server itself — if Claude Desktop / VS Code is connected, ask it to create the task via the `create_task` tool.

---

## Creating a Pull Request

Branch naming: `feature/description`, `fix/description`, `chore/description`

```bash
# 1. Create and switch to a branch
git checkout -b feature/your-feature-name

# 2. Make changes, then commit (follow Conventional Commits)
git add internal/twprojects/yourfile.go
git commit -m "Feature: add new tool for X"

# 3. Push and open PR
git push -u origin feature/your-feature-name
gh pr create \
  --title "Feature: add new tool for X" \
  --body "## Summary
- What changed and why

## Testing
- [ ] Tests pass: \`TWAPI_SERVER=... TWAPI_TOKEN=... go test -v ./...\`
- [ ] Linter passes: \`golangci-lint -c .golangci.yml run ./...\`
- [ ] Linked issue: closes #<number>"
```

PR title prefixes: `Feature:`, `Fix:`, `Docs:`, `Chore:`, `Refactor:`

Check CI status: `gh pr checks` | View PR: `gh pr view --web`

---

## Pushing Docs to the Server

Docs are built with MkDocs and deployed via rsync over SSH. Credentials come from `.env` (see `.env.example`).

### Serve locally first

```bash
./claude/mkdocs-serve.sh
# Visit http://127.0.0.1:8000
```

### Deploy

```bash
./claude/mkdocs-deploy.sh           # build + deploy
./claude/mkdocs-deploy.sh --build   # build only, skip deploy
./claude/mkdocs-deploy.sh --deploy  # deploy existing site/, skip build
```

The script:
1. Reads SSH credentials from `.env`
2. Runs `mkdocs build --clean` from `claude/`
3. rsync-deploys `claude/site/` to `$DOCS_SSH_PATH/site` on the remote

Required `.env` vars for deployment:

| Variable | Description |
|---|---|
| `DOCS_SSH_HOST` | Remote hostname |
| `DOCS_SSH_USER` | SSH username |
| `DOCS_SSH_PRIVATE_KEY` | Path to local private key |
| `DOCS_SSH_PATH` | Remote base path |
| `DOCS_SSH_PORT` | SSH port (default: 22) |

# Tools Reference

## Teamwork Projects Toolset (`internal/twprojects/`)

Each domain file maps to a group of read and write MCP tools:

| File | Domain | Operations |
|---|---|---|
| `projects.go` | Projects | List, Get, Create, Update, Delete |
| `tasks.go` | Tasks | List, Get, Create, Update, Delete |
| `tasklists.go` | Task Lists | List, Get, Create, Update, Delete |
| `users.go` | Users | List, Get |
| `teams.go` | Teams | List, Get, Create, Update |
| `comments.go` | Comments | List, Get, Create, Update, Delete |
| `tags.go` | Tags | List, Get, Create, Update |
| `milestones.go` | Milestones | List, Get, Create, Update, Delete |
| `timelogs.go` | Time Logs | List, Get, Create, Update, Delete |
| `timers.go` | Timers | List, Get, Create, Start, Stop, Delete |
| `activities.go` | Activities | List |
| `companies.go` | Companies | List, Get, Create, Update |
| `notebooks.go` | Notebooks | List, Get, Create, Update, Delete |
| `project_members.go` | Project Members | List, Add, Remove |
| `project_categories.go` | Project Categories | List, Get, Create, Update |
| `workload.go` | Workload | Get |
| `skills.go` | Skills | List, Get |
| `jobroles.go` | Job Roles | List, Get |
| `industries.go` | Industries | List |

## Teamwork Desk Toolset (`internal/twdesk/`)

| File | Domain | Operations |
|---|---|---|
| `tickets.go` | Tickets | List, Get, Create, Update |
| `messages.go` | Messages | List, Get, Create |
| `users.go` | Users | List, Get |
| `inboxes.go` | Inboxes | List, Get |
| `tags.go` | Tags | List, Get, Create |
| `statuses.go` | Statuses | List, Get |
| `files.go` | Files | List, Get, Upload |

## Adding a New Tool

1. Find the relevant domain file (or create one following the existing pattern)
2. Add method registration in that file's `init()` function
3. Implement the handler function using the Teamwork API SDK
4. Decide read vs. write — write tools are excluded in read-only mode
5. Add a test in the corresponding `*_test.go` file

## Read-Only Mode

Set by the caller when creating the `ToolsetGroup`. All write tools (Create, Update, Delete) are simply not registered — no runtime check needed in handlers.

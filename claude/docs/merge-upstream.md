# Merging Upstream Changes

This document covers how to resolve merge conflicts and keep this fork in sync with the upstream `teamwork/mcp` repository.

## Building the Project

Go is **not installed locally**. All builds run inside Docker:

```bash
# Build the HTTP server image
make build

# Build the STDIO server image
make build-stdio
```

To verify the code compiles during development, use the Docker build stage:

```bash
docker buildx build --target runner .
```

---

## Upstream Remote Setup (one-time)

```bash
git remote add upstream https://github.com/teamwork/mcp.git
git fetch upstream
```

---

## Pulling Upstream Changes

### Option 1: Rebase (recommended)

Rebasing replays your commits on top of upstream, so conflicts surface one commit at a time — much easier to resolve than a single big merge commit.

```bash
git fetch upstream
git rebase upstream/main
```

If conflicts arise during rebase:

1. Resolve the conflict in the file
2. `git add <file>`
3. `git rebase --continue`

### Option 2: Merge (current approach)

```bash
git fetch upstream
git merge upstream/main
```

If conflicts arise:

1. Resolve the conflict in the file
2. `git add <file>`
3. `git merge --continue`

Merges work but conflicts compound over time. Keep fork changes in small, scoped commits to reduce the blast radius.

---

## Known Conflict Areas

### `cmd/mcp-http/main.go` — `authMiddleware`

Our fork adds entries to the `whitelistEndpoints` map that upstream does not have. When upstream modifies this map, a conflict will occur.

**Our additions:**

```go
// welcome page is public
"/": {http.MethodGet},
// OAuth2 discovery endpoints are public
"/.well-known/oauth-protected-resource": {http.MethodGet, http.MethodOptions},
```

**Resolution:** Keep our entries and merge in any new upstream entries. Do not drop either side.

---

## Tips for Reducing Future Conflicts

- Keep fork-specific changes in clearly named, small commits so `git blame` makes the intent obvious.
- When upstream changes a file we've also touched, compare diffs carefully — upstream may have refactored the same logic in a different direction.
- After resolving a conflict, leave a comment in the code (or update this doc) noting what was preserved and why.

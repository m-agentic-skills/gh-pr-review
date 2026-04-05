# Step 00: Pre-flight

Run this before anything else. If it fails, stop immediately — do not continue to any other step.

All commands in this step run from `{project-root}`.

## Check

### 1. Verify required tools are installed

```
git --version
```

If this fails: stop and tell the user: "`git` is not installed. Install it first."

```
gh --version
```

If this fails: stop and tell the user: "`gh` CLI is not installed. Install it from https://cli.github.com then re-run."

### 2. Verify GitHub repo identity

```
gh repo view --json name,nameWithOwner
```

This single command covers all failure cases:

| What went wrong | Error contains | Tell the user |
|---|---|---|
| `gh` not installed | `command not found` / `not recognized` | "`gh` CLI is not installed. Install it from https://cli.github.com then re-run." |
| Not in a git repo | `not a git repository` | "This directory is not a git repository." |
| No GitHub remote | `Could not resolve` / `no git remote` | "This repo does not have a GitHub remote. Push it to GitHub first." |
| Not authenticated | `authentication` / `401` / `log in` | "Not authenticated with GitHub. Run `gh auth login` then re-run." |

If the command succeeds (exit 0): read `.name` and `.nameWithOwner` from the JSON output and pass them to step-01 as `REPO_NAME` and `OWNER_REPO`. Continue.

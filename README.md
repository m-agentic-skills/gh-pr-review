# gh-pr-review

AI skill for reviewing GitHub pull requests in a team repo — with honest analysis and per-PR review notes.

Part of the **gh-custom-flow** suite alongside [gh-feature](../gh-feature), [gh-submit-pr](../gh-submit-pr), and [gh-deploy](../gh-deploy).

## What it does

Say "review my prs" and the skill will:

1. List all PRs assigned to you for review
2. Fetch the diff for the one you select
3. Read local `AGENTS.md` for team standards, and `~/gh-custom-flow/{repo}/pr-reviews/` for past review notes
4. Give an honest three-section analysis: what looks good, what could be improved, what it's unsure about
5. Discuss with you — you can agree, push back, or add your own points
6. Post comments via `gh pr comment` (shown and confirmed before each)
7. Submit your review decision: approve, request changes, or comment
8. Write full review notes to `~/gh-custom-flow/{repo}/pr-reviews/pr_{number}.md`

## Trigger phrases

**Review:** "review my prs", "review pr", "check assigned prs", "assigned prs"

## Prerequisites

- **Python 3.x** — for `config_helper.py`
- **gh CLI** — `gh --version` ([install](https://cli.github.com))
- **gh auth login** — authenticated with GitHub

## Install

**macOS / Linux**

```bash
git clone https://github.com/muthuishere/gh-pr-review.git
cd gh-pr-review
bash install.sh
```

**Windows**

```cmd
git clone https://github.com/muthuishere/gh-pr-review.git
cd gh-pr-review
install.cmd
```

## Uninstall

**macOS / Linux:** `bash uninstall.sh`
**Windows:** `uninstall.cmd`

## Review notes

After each review, full notes are written to:

```
~/gh-custom-flow/{reponame}/pr-reviews/pr_{number}.md
```

These are read automatically on the next review of the same repo, so the skill learns your team's patterns over time.

## Part of gh-custom-flow

| Skill | What it does |
|---|---|
| [gh-feature](../gh-feature) | Create feature/issue/bug branches |
| [gh-submit-pr](../gh-submit-pr) | Commit, push, and create PRs for finished branch work |
| **gh-pr-review** | Review pull requests |
| [gh-deploy](../gh-deploy) | Trigger GitHub Actions deployment workflows |

All four skills share `~/gh-custom-flow/{reponame}/config.json`.

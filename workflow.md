---
name: gh-pr-review-workflow
---

# GH PR Review Workflow

One job: review PRs well.

## Variables

- `{project-root}` = the user's active project folder (where they invoked this skill). All `gh` and `git` commands must be run from this directory. In Claude Code this is the working directory when the skill is triggered.
- `{skill-root}` = the installed folder of this skill (where `scripts/`, `steps/`, `references/` live).
- `{config-dir}` = `~/config/.m-agent-skills/{reponame}/`

## Core Rules

- Run every `gh` and `git` command from `{project-root}`.
- Show every command before running it. Wait for confirmation.
- For review: be honest. Three sections — good, improvable, uncertain. No bluffing.
- pr-reviews/ files are the memory — one file per PR, written after every review.

## Process

1. Read `steps/step-00-preflight.md` — verify `gh` is installed and this is a GitHub repo. Stop here if not.
2. Read `references/activation-routing.xml` — confirm this is a review-pr request.
3. Read `steps/step-01-init.md` — load config.
4. Read `steps/step-03-review-pr.md` — for review my prs / review pr.

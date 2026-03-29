---
name: gh-pr-review
description: Review assigned pull requests in GitHub team repos. Lists assigned PRs, analyzes the diff against local AGENTS.md, gives an honest assessment, posts comments via gh, and submits approve/request-changes/comment — saving review insights to pr-memories.md for future reviews. Use when the user says "review my prs", "review pr", "check assigned prs", or any request to review a pull request.
---

# GH PR Review

Use this skill when the user wants to review assigned pull requests in a GitHub team repo.

This skill:

- verifies `gh` is available and the current folder is a GitHub repo
- reads the default branch from repo config for context
- lists assigned PRs
- inspects the diff with local repo context
- produces an honest review outcome
- posts comments and submits the review through `gh`
- stores review memory in `pr-memories.md` for future context

Follow the instructions in `./workflow.md`.

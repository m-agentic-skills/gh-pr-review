# Step 02: Create Pull Request

## Pre-flight

Get current branch:

```
git branch --show-current
```

If result equals `{DEFAULT_BRANCH}`, stop:
> "You are on `{DEFAULT_BRANCH}`. Switch to a feature branch first."

## Get Commits

```
git log origin/{DEFAULT_BRANCH}..HEAD --oneline
```

Show the commit list. If empty, stop:
> "No commits ahead of `{DEFAULT_BRANCH}` yet — nothing to open a PR for."

## Draft Title and Body

- **Title**: most descriptive single commit message, under 72 characters.
- **Body**: bullet list of all commits under a `## Summary` heading.

Show the draft and ask:
> "Here's the draft PR:
>
> **Title:** `{title}`
>
> **Body:**
> ```
> {body}
> ```
>
> Looks good, or would you like to change anything?"

Wait for confirmation or edits before continuing.

## Create the PR

Show and confirm before running:

```
gh pr create --base {DEFAULT_BRANCH} --head {CURRENT_BRANCH} --title "{title}" --body "{body}"
```

## After Completion

Show the PR URL from `gh pr create` output:
> "PR created: {PR_URL}"

Offer:
> "To trigger a deployment, use the **gh-deploy** skill."

## Edge Cases

- PR already exists: report the error, suggest `gh pr view` to find it.
- Not authenticated: `gh auth login`.

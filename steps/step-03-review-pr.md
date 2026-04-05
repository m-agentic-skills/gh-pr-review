# Step 03: Review PR

Seven phases: List → Select → Analyze → Discuss → Comment → Submit → Write

`{skill-root}` = installed root folder of this skill.

---

## Phase 1: List PRs for Review

```
gh pr list --search "review-requested:@me" --json number,title,author,headRefName,additions,deletions
```

If empty, try:

```
gh pr list --assignee @me --json number,title,author,headRefName,additions,deletions
```

Display as numbered list:
```
1. #42  Add user auth  (feature/user-auth)  by alice  +120 -30
2. #38  Fix timeout    (fix/login-timeout)  by bob    +15  -5
```

Ask: "Which PR would you like to review? Enter the number."

---

## Phase 2: Fetch Details and Diff

Show and confirm before running each:

```
gh pr view {PR_NUMBER} --json number,title,body,author,baseRefName,headRefName,additions,deletions,changedFiles
```

```
gh pr diff {PR_NUMBER}
```

Read the full diff. Note files changed and nature of changes.

---

## Phase 3: Load Context

**AGENTS.md** — look in current dir and repo root. If found, read it. It defines the team's coding standards and review expectations. If not found, note it — do not invent standards.

**Previous PR reviews** — check `~/config/.m-agent-skills/{REPO_NAME}/pr-reviews/`. If the directory exists, list the files (`pr_*.md`). Read the most recent 2–3 files to pick up recurring patterns, team preferences, and past corrections. Do not quote them verbatim — use them to inform your analysis silently. If `pr_{PR_NUMBER}.md` already exists for this PR (a previous partial review), read it first — it takes priority.

---

## Phase 4: Analyze — Be Honest

Three sections, no padding:

### What looks good
Specific things done well — reference file names or AGENTS.md standards met.

### What could be improved
Concrete issues: missing tests, unclear naming, logic concerns, AGENTS.md violations.
Include file name and rough line range from the diff where possible. Rank by severity.

### What I'm not sure about
Be direct about missing context. Examples: "I don't know the full domain model here", "AGENTS.md doesn't cover this case", "I can't tell if this simplification is deliberate."
Do not guess or bluff in this section.

Show the analysis and ask:
> "What do you think? Anything to add, remove, or correct before I post comments?"

---

## Phase 5: Discuss and Build Comment List

Wait for the user's response. They may agree, push back, add points, or change severity.

Update the comment list based on the conversation. Show a final list before posting:

```
COMMENT 1 — file: src/auth.py ~line 42
  "The token expiry is hardcoded. Consider env var."

COMMENT 2 — general
  "Good separation of concerns in the service layer."
```

Ask: "Ready to post these? Any changes?"

---

## Phase 6: Post Comments

For each comment, show and confirm before posting.

**General PR comment** (always works, use when line position is unclear):

```
gh pr comment {PR_NUMBER} --body "{comment_body}"
```

**Line-level review comment** (use only when you can pinpoint the diff position):

```
gh api repos/{OWNER_REPO}/pulls/{PR_NUMBER}/reviews \
  -f body="" \
  -f event="COMMENT" \
  -f "comments[][path]={filepath}" \
  -f "comments[][position]={diff_line_position}" \
  -f "comments[][body]={comment_body}"
```

Note: `position` is the line number in the unified diff output, not the file line number. If unsure, use a general comment and tell the user: "Posting as a general comment — I can't pin the exact diff line."

---

## Phase 7: Submit Review Decision

Ask:
> "What would you like to submit?
> 1. Approve
> 2. Request changes
> 3. Comment only (no decision yet)"

Show and confirm the command:

**Approve:**
```
gh pr review {PR_NUMBER} --approve --body "{summary}"
```

**Request changes:**
```
gh pr review {PR_NUMBER} --request-changes --body "{what needs fixing}"
```

**Comment only:**
```
gh pr review {PR_NUMBER} --comment --body "{summary}"
```

---

## Phase 8: Write PR Review File

Write (or overwrite if it exists) `~/config/.m-agent-skills/{REPO_NAME}/pr-reviews/pr_{PR_NUMBER}.md`.

Create the `pr-reviews/` directory if it does not exist.

Full file format:

```markdown
# PR #{PR_NUMBER} — {title}

**Repo:** {REPO_NAME}
**Author:** {author}
**Branch:** {headRefName} → {baseRefName}
**Reviewed:** {YYYY-MM-DD}
**Decision:** {approve | request-changes | comment}
**Changes:** +{additions} -{deletions} across {changedFiles} files

---

## What Looks Good

- {bullet per item — be specific, reference file names}

## What Could Be Improved

- {bullet per comment posted — include file and rough line if known}

## Uncertain / Needs Context

- {bullet per area where you lacked enough information to judge}

## User Corrections

- {anything the user told you that changed your initial analysis — important for learning}

## Comments Posted

- {list each comment body, labelled general or file:line}

---

*Reviewed with gh-pr-review skill*
```

Confirm to the user:
> "Review written to `~/config/.m-agent-skills/{REPO_NAME}/pr-reviews/pr_{PR_NUMBER}.md`"

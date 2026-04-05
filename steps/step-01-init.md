# Step 01: Init — Load Config

`{skill-root}` = installed root folder of this skill.

## Inputs from Pre-flight

`REPO_NAME` and `OWNER_REPO` are already set by step-00. Use them directly.

## Shared Config Folder Layout

All three skills read and write to the same folder:
```
~/config/.m-agent-skills/{reponame}/
├── config.json          ← shared preferences (default_branch, deploy_workflow)
└── pr-reviews/
    └── pr_42.md         ← one file per PR review (written by this skill)
```

## Load Config

```
python {skill-root}/scripts/config_helper.py read {REPO_NAME}
```

- `NOT_FOUND` → for create-pr, `default_branch` is required. Ask:
  > "What is your team's default branch? (press Enter to use `dev`)"
  Then: `python {skill-root}/scripts/config_helper.py set {REPO_NAME} default_branch {VALUE}`
- JSON output → use stored values.

## Output

- `REPO_NAME`, `OWNER_REPO`, `DEFAULT_BRANCH`

---
description: Generate a comprehensive PR description using the pr-description-writer Skill.
---

Use your `pr-description-writer` Skill to create or update a PR description.

## Automatic Workflow

Follow this sequence to gather context and generate the description:

### 1. Detect PR Status

```bash
# Check if current branch has a PR
gh pr view --json number,title,url,baseRefName 2>/dev/null
```

- If exit code is `0`: PR exists → you'll update it
- If exit code is non-zero: No PR yet → you'll help create one

### 2. Identify Base Branch (Smart Detection)

```bash
# Priority order for detecting base branch:

# 1. If PR exists, use its base
gh pr view --json baseRefName --jq '.baseRefName' 2>/dev/null

# 2. Get repo's default branch via GitHub API
gh repo view --json defaultBranchRef --jq '.defaultBranchRef.name'

# 3. Check git remote HEAD
git remote show origin 2>/dev/null | grep "HEAD branch" | cut -d: -f2 | xargs

# 4. Check for common branches (main, master, release, develop)
git branch -r | grep -E "origin/(main|master|release|develop)$" | head -1
```

**Important**: Don't assume `release` or `main` - always detect!

### 3. Gather ALL Changes

**CRITICAL**: Include everything that will be in the PR:

```bash
BASE="origin/release"  # adjust based on step 2

# All commits in the branch
git log ${BASE}..HEAD --oneline

# Full diff (committed changes)
git diff ${BASE}...HEAD --stat

# Any uncommitted changes
git status --short
git diff --stat           # unstaged
git diff --cached --stat  # staged
```

### 4. Get Existing PR Details (if updating)

```bash
gh pr view --json body,commits,files
```

### 5. Generate Description

Using the Skill's PR description structure:
- Summary with feature table (if 3+ features)
- Visual diagrams for flows
- Detailed sections per feature
- Collapsible file lists
- Test commands + manual steps
- Breaking changes / notes

### 6. Update or Create PR

```bash
# Update existing PR
gh pr edit --body "$(cat <<'EOF'
## Summary
...
EOF
)"

# Or create new PR
gh pr create --title "Title" --body "..." --base release
```

## Arguments

- `<pr-number>` (optional): Specific PR to update. If omitted, uses current
  branch's PR or prepares description for a new PR.
- `--update`: Automatically update the PR without confirmation.
- `--create`: Create a new PR with the generated description.

## Examples

```bash
# Auto-detect PR status and generate description
/pr-description-writer:write-pr

# Update existing PR #1234
/pr-description-writer:write-pr 1234

# Update PR automatically without confirmation
/pr-description-writer:write-pr --update

# Create new PR with generated description
/pr-description-writer:write-pr --create
```

## Key Reminder

**Always analyze ALL changes in the branch**, not just the latest commit:
- Use `git log origin/release..HEAD` for commit history
- Use `git diff origin/release...HEAD` for full diff
- Include uncommitted changes if the user plans to commit them

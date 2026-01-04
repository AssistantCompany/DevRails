---
description: Create a pull request with proper template, description, and issue linking
allowed-tools: Bash, Read, Grep, Glob
---

# Create Pull Request

You are creating a pull request. Follow the PR workflow from the org standards.

## Steps

1. **Check current state**
   - Run `git status` to verify:
     - Not on `main` branch
     - All changes committed
     - Branch is ahead of remote (or needs push)

2. **Gather context**
   - Run `git log main..HEAD --oneline` to see commits in this branch
   - Run `git diff main...HEAD --stat` to see files changed
   - Identify the type of change (feature, bugfix, task, chore)

3. **Push branch if needed**
   - If branch not pushed: `git push -u origin <branch-name>`

4. **Create PR using gh CLI**
   ```bash
   gh pr create --title "<type>: <description>" --body "$(cat <<'EOF'
   ## Summary
   <1-3 bullet points explaining what this PR does>

   ## Changes
   <list of key changes>

   ## Test Plan
   - [ ] <how to test this change>

   ## Related Issues
   Fixes #<issue-number> (if applicable)

   ---
   Generated with Claude Code
   EOF
   )"
   ```

5. **Determine PR title**
   - For bugfix branches: `fix: <description>`
   - For feature branches: `feat: <description>`
   - For task branches: `chore: <description>`

6. **Link issues if applicable**
   - If branch name contains issue number, link it
   - Use `Fixes #123` for bugs that close issues
   - Use `Related to #123` for features

7. **Report result**
   - Show the PR URL
   - Mention if CI will run
   - Suggest requesting reviewers

## Reference
PR template: docs/dev/templates/pull-request-template.md
PR workflow: docs/dev/standards/pull-request-workflow.md

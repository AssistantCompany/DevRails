---
description: Start bugfix workflow - creates branch, investigates issue, implements fix with tests
allowed-tools: Bash, Read, Edit, Write, Grep, Glob, Task
argument-hint: <bug-description>
---

# Bugfix Workflow

You are starting a bugfix workflow. Follow the defect workflow from the org standards.

## Arguments
Bug description: $ARGUMENTS

## Steps

1. **Check current state**
   - Run `git status` to see current branch and changes
   - If on `main` branch, proceed to create bugfix branch
   - If uncommitted changes exist, ask user how to handle them

2. **Create bugfix branch**
   - Sanitize the description to kebab-case (lowercase, hyphens, no special chars)
   - Create branch: `git checkout -b bugfix/<sanitized-description>`
   - Example: "null pointer in auth" → `bugfix/null-pointer-in-auth`

3. **Investigate the issue**
   - Search for relevant code using Grep/Glob
   - Read the affected files
   - Identify root cause

4. **Implement fix**
   - Make minimal, focused changes
   - Fix the root cause, not just symptoms
   - Avoid introducing new issues

5. **Add regression test**
   - Create or update test that would have caught this bug
   - Ensure test fails without the fix, passes with it

6. **Commit with conventional format**
   ```
   fix: <short description>

   <explanation of what was broken and how it's fixed>

   Fixes #<issue-number-if-applicable>
   ```

7. **Offer next steps**
   - Ask if user wants to create a PR now (`/pr`)
   - Or continue working on more changes

## Reference
Full workflow details: docs/dev/standards/defect-workflow.md
Branch naming: docs/dev/standards/git-workflow.md
Commit format: docs/dev/templates/commit-message-template.md

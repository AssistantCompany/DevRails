---
description: Start feature workflow - creates branch, implements new capability with tests
allowed-tools: Bash, Read, Edit, Write, Grep, Glob, Task
argument-hint: <feature-description>
---

# Feature Workflow

You are starting a feature workflow. Follow the PR workflow from the org standards.

## Arguments
Feature description: $ARGUMENTS

## Steps

1. **Check current state**
   - Run `git status` to see current branch and changes
   - If on `main` branch, proceed to create feature branch
   - If uncommitted changes exist, ask user how to handle them

2. **Create feature branch**
   - Sanitize the description to kebab-case (lowercase, hyphens, no special chars)
   - Create branch: `git checkout -b feature/<sanitized-description>`
   - Example: "add dark mode" → `feature/add-dark-mode`

3. **Understand the scope**
   - Ask clarifying questions if the feature is ambiguous
   - Identify which files/components will be affected
   - Consider if this should be broken into smaller PRs

4. **Implement feature**
   - Follow existing code patterns in the project
   - Keep changes focused on the feature
   - Avoid unrelated refactoring in the same branch

5. **Add tests**
   - Unit tests for new functions/components
   - Integration tests if applicable
   - Ensure existing tests still pass

6. **Commit with conventional format**
   ```
   feat: <short description>

   <explanation of what the feature does and why>
   ```

7. **Offer next steps**
   - Ask if user wants to create a PR now (`/pr`)
   - Or continue working on more changes

## Reference
Full workflow details: docs/dev/standards/pull-request-workflow.md
Branch naming: docs/dev/standards/git-workflow.md
Commit format: docs/dev/templates/commit-message-template.md

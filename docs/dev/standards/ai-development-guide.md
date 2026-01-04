# AI Development Guide

> Guidelines for AI-assisted development using Claude Code.

---

## First Steps

Before starting any work in this organization:

1. **Check org-level CLAUDE.md** at the repository root
2. **Read these standards** at `docs/dev/`
3. **Review the glossary** at `docs/dev/definitions/glossary.md`
4. **Identify work type** - Is this a defect, feature, task, or chore?

---

## Key Principles

### 1. Follow Existing Patterns
- Observe how existing code is structured
- Match naming conventions
- Use established libraries and utilities
- Don't introduce new patterns without discussion

### 2. Use Consistent Terminology
Always use terms from the [glossary](../definitions/glossary.md):
- PR = Pull Request (container for changes)
- Defect = Bug (broken functionality)
- Feature = New capability
- Branch = Isolated workspace

### 3. One Branch = One PR = One Unit of Work
- Create a branch for each distinct task
- Don't mix unrelated changes
- Keep PRs focused and reviewable

### 4. Link to Issues
When fixing defects or implementing features:
- Reference the GitHub Issue
- Use `Fixes #123` in PR description
- Provide context for reviewers

---

## Workflow by Task Type

### For Defects (Bugs)

Follow [defect-workflow.md](./defect-workflow.md):

1. Verify issue exists in GitHub Issues
2. Create branch: `bugfix/issue-123-description`
3. Fix the root cause
4. Add regression test
5. Open PR with `Fixes #123`
6. Get review approval
7. Merge when CI passes

### For Features

Follow [pull-request-workflow.md](./pull-request-workflow.md):

1. Create branch: `feature/description`
2. Implement feature
3. Add tests
4. Open PR with clear description
5. Get review approval
6. Merge when CI passes

### For Tasks/Chores

1. Create branch: `task/description` or `chore/description`
2. Make changes
3. Open PR
4. Get review
5. Merge

---

## Before Making Changes

### Always Read First
- Read existing code before modifying
- Understand context and patterns
- Check for related functionality

### Check for Existing Solutions
- Search codebase for similar functionality
- Look for utility functions
- Check if helper exists before creating new one

### Consider Impact
- What else might this change affect?
- Are there tests to update?
- Does documentation need updating?

---

## During Development

### Follow Commit Conventions
Use conventional commit format:
```
type: short description

Optional body explaining why.
```

Types: `feat`, `fix`, `docs`, `style`, `refactor`, `test`, `chore`

### Keep Changes Focused
- One logical change per commit
- Small, reviewable PRs
- Don't mix refactoring with features

### Test Your Changes
- Run existing tests
- Add tests for new code
- Verify manually when appropriate

---

## PR Creation

### Use Templates
Use templates from `docs/dev/templates/`:
- [pull-request-template.md](../templates/pull-request-template.md)
- Link to issues when applicable

### Write Good Descriptions
- Explain **what** changed
- Explain **why** it changed
- Include test plan
- Add screenshots for UI changes

### Self-Review First
Before requesting review:
- [ ] Code compiles without errors
- [ ] Tests pass
- [ ] Linting passes
- [ ] Self-reviewed the diff
- [ ] Description is complete

---

## Project Integration

### Key Principle: Merge, Don't Replace

When integrating with projects, **never override existing content**:
- Existing CLAUDE.md → ADD breadcrumb section, keep all existing content
- Existing .github/ templates → Keep existing, don't replace
- Existing README.md → Keep existing, optionally add link

### New Project (Greenfield)
When working on a project without CLAUDE.md:

1. Create `CLAUDE.md` using [project-claude-md.template](../templates/project-claude-md.template)
2. Customize with project-specific details
3. Include build/run commands
4. Document architecture

### Existing Project (Brownfield)
When CLAUDE.md already exists:

1. **Do NOT replace** the existing file
2. **ADD** the breadcrumb section from [BREADCRUMB_TEMPLATE.md](../BREADCRUMB_TEMPLATE.md)
3. Insert near the top, after the title
4. Keep all existing project-specific content

Example:
```markdown
# CLAUDE.md                      <-- Keep existing title

## Organization Standards        <-- ADD this section
This project follows the shared development standards.
See: ../../docs/dev/README.md
[rest of breadcrumb...]

## Build Commands                <-- Keep existing content
[existing project content...]
```

### Existing .github/ Templates
If project has existing GitHub templates:
- **Keep the project's templates** - they may have project-specific customizations
- Org templates are references, not replacements

---

## Common Tasks

### Creating a Branch
```bash
git checkout main
git pull
git checkout -b <prefix>/<description>
```

### Making a Commit
```bash
git add .
git commit -m "type: description"
```

### Opening a PR
1. Push branch: `git push -u origin branch-name`
2. Go to GitHub
3. Click "Compare & pull request"
4. Fill in template
5. Request reviewers

### Fixing a Bug
```bash
# Branch
git checkout -b bugfix/issue-123-fix-thing

# Fix + test
# Commit
git commit -m "fix: prevent null pointer in login

Added null check for user object before accessing properties.

Fixes #123"

# Push and PR
git push -u origin bugfix/issue-123-fix-thing
```

---

## What Not to Do

### Never
- Commit directly to main
- Push without testing
- Skip the PR process
- Ignore CI failures
- Force push shared branches
- Commit secrets or credentials
- Amend pushed commits without good reason

### Avoid
- Giant PRs (> 400 lines)
- Mixing unrelated changes
- Vague commit messages
- Skipping code review
- Ignoring linting errors

---

## Communication

### In PRs
- Respond to all review comments
- Explain reasoning when disagreeing
- Thank reviewers

### In Commits
- Use imperative mood ("Add feature" not "Added feature")
- Keep first line under 72 characters
- Reference issues when applicable

### In Code
- Use clear variable names
- Comment complex logic (not obvious code)
- Document public APIs

---

## Resources

### Standards (This Package)
- [PR Workflow](./pull-request-workflow.md)
- [Defect Workflow](./defect-workflow.md)
- [Git Workflow](./git-workflow.md)
- [GitHub Actions](./github-actions-standards.md)
- [Code Review](./code-review-standards.md)

### Definitions
- [Glossary](../definitions/glossary.md)
- [Work Types](../definitions/work-types.md)

### Templates
- [PR Template](../templates/pull-request-template.md)
- [Bug Report](../templates/bug-report-template.md)
- [Feature Request](../templates/feature-request-template.md)
- [Commit Message](../templates/commit-message-template.md)

---

## Quick Reference

```bash
# Start work
git checkout main && git pull
git checkout -b <type>/<description>

# Develop
# Edit files, run tests
git add . && git commit -m "type: description"

# Push and PR
git push -u origin branch-name
# Create PR on GitHub

# After merge
git checkout main && git pull
git branch -d branch-name
```

**Commit Types:**
- `feat:` new feature
- `fix:` bug fix
- `docs:` documentation
- `test:` tests
- `chore:` maintenance
- `refactor:` restructure

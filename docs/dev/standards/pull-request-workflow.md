# Pull Request Workflow

> Complete guide to the PR lifecycle from branch creation to merge.

---

## What is a Pull Request?

A **Pull Request (PR)** is:
- A request to merge code changes from one branch into another
- A container for code changes that includes review and discussion
- A gate that ensures code is reviewed before joining the main codebase

> **Key Understanding**: A PR is the **container** for code changes, not the problem itself. Bugs and features are tracked as Issues; PRs are how we implement the solution.

---

## The PR Lifecycle

```
┌─────────────────────────────────────────────────────────────────┐
│  1. Create Branch                                               │
│     └── git checkout -b feature/my-feature                     │
│                                                                 │
│  2. Make Changes                                                │
│     └── Edit files, add tests, commit                          │
│                                                                 │
│  3. Push to Remote                                              │
│     └── git push -u origin feature/my-feature                  │
│                                                                 │
│  4. Open PR                                                     │
│     └── GitHub: "Compare & pull request"                       │
│                                                                 │
│  5. Review Cycle                                                │
│     └── Reviewers comment/approve/request changes              │
│                                                                 │
│  6. Address Feedback                                            │
│     └── Push more commits to same branch                       │
│                                                                 │
│  7. Merge                                                       │
│     └── Squash and merge (recommended)                         │
│                                                                 │
│  8. Clean Up                                                    │
│     └── Delete branch                                          │
└─────────────────────────────────────────────────────────────────┘
```

---

## Step-by-Step Guide

### 1. Create a Branch

**Rule: One branch per PR**

```bash
# Make sure you're on main and up to date
git checkout main
git pull

# Create and switch to new branch
git checkout -b <prefix>/<description>
```

**Branch Naming Convention:**
| Prefix | Use For | Example |
|--------|---------|---------|
| `feature/` | New functionality | `feature/add-dark-mode` |
| `bugfix/` | Bug fixes | `bugfix/fix-login-crash` |
| `task/` | Technical tasks | `task/upgrade-dependencies` |
| `chore/` | Maintenance | `chore/cleanup-logs` |

**With Issue Numbers:**
```
bugfix/issue-123-fix-login
feature/JIRA-456-add-search
```

### 2. Make Changes

```bash
# Edit files
# Run tests locally
# Check linting

# Stage changes
git add .

# Commit with descriptive message
git commit -m "feat: add dark mode toggle

- Add theme context provider
- Create toggle component
- Add localStorage persistence"
```

### 3. Push to Remote

```bash
# First push (sets upstream)
git push -u origin feature/my-feature

# Subsequent pushes
git push
```

### 4. Open the PR

On GitHub:
1. Navigate to your repository
2. Click "Compare & pull request" (or "Pull requests" → "New pull request")
3. Select base branch (usually `main`)
4. Select compare branch (your feature branch)
5. Fill in PR template:

```markdown
## Summary
- Brief description of changes

## Type of Change
- [ ] Feature
- [ ] Bug fix
- [ ] Refactor

## Related Issues
Fixes #123

## Test Plan
- [ ] Unit tests pass
- [ ] Manual testing completed

## Screenshots (if applicable)
```

### 5. Review Cycle

**What Reviewers Look For:**
- Code correctness
- Test coverage
- Performance implications
- Security concerns
- Code style consistency
- Documentation updates

**Review Actions:**
| Action | Meaning |
|--------|---------|
| Comment | Questions or suggestions |
| Approve | Ready to merge |
| Request Changes | Must be addressed before merge |

### 6. Address Feedback

When changes are requested:

```bash
# Make the requested changes
# Commit them
git add .
git commit -m "fix: address review feedback

- Renamed variable for clarity
- Added missing test case"

# Push to the same branch - PR updates automatically
git push
```

**Important:** Push to the **same branch**. The PR updates automatically with new commits.

### 7. Merge

Once approved and CI passes:

**Merge Strategies:**
| Strategy | Description | When to Use |
|----------|-------------|-------------|
| Squash and Merge | Combines all commits into one | **Default** - keeps history clean |
| Rebase and Merge | Linear history, preserves commits | When individual commits matter |
| Merge Commit | Creates merge commit | Rarely used |

**Recommended: Squash and Merge**

### 8. Clean Up

After merging:
- Delete the feature branch (GitHub offers this automatically)
- Locally: `git checkout main && git pull && git branch -d feature/my-feature`

---

## Best Practices

### Keep PRs Small
- Easier to review
- Faster to merge
- Less risk of conflicts
- **Aim for < 400 lines changed**

### Write Good PR Descriptions
- Explain **why**, not just what
- Link to related issues
- Include test plan
- Add screenshots for UI changes

### Respond to Reviews Promptly
- Address feedback quickly
- Explain your reasoning if you disagree
- Thank reviewers

### Keep Branch Updated
```bash
# If main has moved ahead
git checkout main
git pull
git checkout feature/my-feature
git rebase main
git push --force-with-lease
```

---

## PR vs Issue

| Aspect | Issue | PR |
|--------|-------|-----|
| What it is | Problem or request | Proposed solution |
| Created when | Bug found or feature needed | Ready to propose code |
| Contains | Description, reproduction steps | Code changes, tests |
| Action | Assigned, prioritized | Reviewed, merged |

**Flow:**
```
Issue (problem) → Branch (work) → PR (solution) → Merge (done)
```

---

## Common Mistakes to Avoid

1. **Direct commits to main** - Always use PRs
2. **Giant PRs** - Split into smaller, focused changes
3. **No tests** - Include tests for all changes
4. **Vague descriptions** - Be specific about what and why
5. **Ignoring CI failures** - Fix before requesting review
6. **Force pushing shared branches** - Only on your own branches

---

## Quick Commands Reference

```bash
# Start new work
git checkout main && git pull
git checkout -b feature/my-feature

# Regular workflow
git add .
git commit -m "type: description"
git push

# Update from main
git fetch origin
git rebase origin/main
git push --force-with-lease

# After merge
git checkout main && git pull
git branch -d feature/my-feature
```

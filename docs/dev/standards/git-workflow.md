# Git Workflow

> Branch strategy, commit conventions, and Git best practices.

---

## Branch Strategy

### Main Branch
- `main` is the primary branch
- Always deployable
- Protected - no direct commits
- All changes via Pull Requests

### Feature Branches
One branch per unit of work:

```
main
 ├── feature/add-dark-mode
 ├── bugfix/issue-123-fix-login
 ├── task/upgrade-dependencies
 └── chore/cleanup-logs
```

---

## Branch Naming Convention

### Format
```
<prefix>/<description>
<prefix>/issue-<number>-<description>
```

### Prefixes

| Prefix | Use For | Example |
|--------|---------|---------|
| `feature/` | New functionality | `feature/add-user-auth` |
| `bugfix/` | Bug fixes | `bugfix/fix-login-crash` |
| `task/` | Technical work | `task/add-ci-pipeline` |
| `chore/` | Maintenance | `chore/update-deps` |
| `hotfix/` | Urgent production fix | `hotfix/security-patch` |
| `spike/` | Research/exploration | `spike/evaluate-redis` |

### Good Examples
```
feature/add-dark-mode-toggle
bugfix/issue-42-fix-safari-login
task/upgrade-node-to-20
chore/remove-unused-deps
hotfix/fix-payment-gateway
```

### Bad Examples
```
fix                    # Too vague
my-branch              # Not descriptive
feature-123            # Missing description
Feature/Add-Thing      # Wrong casing
```

---

## Commit Messages

### Format

```
<type>: <short description>

[optional body]

[optional footer]
```

### Types

| Type | Description | Example |
|------|-------------|---------|
| `feat` | New feature | `feat: add dark mode toggle` |
| `fix` | Bug fix | `fix: resolve login crash` |
| `docs` | Documentation | `docs: update API docs` |
| `style` | Formatting | `style: fix indentation` |
| `refactor` | Code restructure | `refactor: simplify auth flow` |
| `test` | Tests | `test: add login tests` |
| `chore` | Maintenance | `chore: update deps` |
| `build` | Build system | `build: upgrade webpack` |
| `ci` | CI/CD changes | `ci: add deploy workflow` |
| `perf` | Performance | `perf: optimize query` |

### Good Examples

```bash
# Short and clear
feat: add user authentication

# With body for complex changes
fix: prevent crash on empty input

The input field was not validating for empty strings,
causing a null reference exception when submitted.

Added null check and user-friendly error message.

Fixes #123

# With scope
feat(auth): add OAuth2 support
fix(api): handle rate limiting
```

### Bad Examples

```bash
# Too vague
update code
fix stuff
WIP

# Too long first line
Added a new feature that allows users to toggle dark mode and persist their preference

# Missing type
add dark mode
```

### Rules

1. **First line ≤ 72 characters**
2. **Use imperative mood**: "add" not "added"
3. **No period at end of first line**
4. **Separate body with blank line**
5. **Explain why, not what** (code shows what)

---

## Common Workflows

### Starting New Work

```bash
# Ensure main is up to date
git checkout main
git pull

# Create and switch to new branch
git checkout -b feature/my-feature
```

### Regular Development

```bash
# Stage changes
git add .

# Or stage specific files
git add src/component.js

# Commit
git commit -m "feat: add new component"

# Push (first time)
git push -u origin feature/my-feature

# Push (subsequent)
git push
```

### Keeping Branch Updated

```bash
# Option 1: Rebase (preferred - linear history)
git fetch origin
git rebase origin/main

# Option 2: Merge (if conflicts are complex)
git fetch origin
git merge origin/main
```

### After PR Merge

```bash
# Switch to main
git checkout main

# Pull latest
git pull

# Delete local branch
git branch -d feature/my-feature
```

---

## Handling Conflicts

### During Rebase

```bash
# Start rebase
git rebase origin/main

# If conflicts:
# 1. Edit conflicting files
# 2. Stage resolved files
git add <file>

# 3. Continue rebase
git rebase --continue

# Or abort if needed
git rebase --abort
```

### Conflict Markers

```
<<<<<<< HEAD
Your changes
=======
Changes from main
>>>>>>> main
```

1. Edit file to resolve
2. Remove conflict markers
3. Keep the correct code
4. Stage and continue

---

## Interactive Rebase (Cleaning Up)

Before opening a PR, clean up commits:

```bash
# Rebase last N commits
git rebase -i HEAD~3

# In editor:
pick abc123 first commit
squash def456 second commit  # Combine with previous
squash ghi789 third commit   # Combine with previous
```

**Commands:**
- `pick` - Keep commit
- `squash` - Combine with previous
- `reword` - Edit message
- `drop` - Remove commit

---

## Undoing Things

### Undo Last Commit (keep changes)
```bash
git reset --soft HEAD~1
```

### Undo Last Commit (discard changes)
```bash
git reset --hard HEAD~1
```

### Undo Staged Changes
```bash
git restore --staged <file>
```

### Undo Working Directory Changes
```bash
git restore <file>
```

### Revert a Pushed Commit
```bash
git revert <commit-hash>
git push
```

---

## Stashing

Save work temporarily:

```bash
# Stash current changes
git stash

# Stash with message
git stash push -m "WIP: feature X"

# List stashes
git stash list

# Apply most recent stash
git stash pop

# Apply specific stash
git stash apply stash@{2}

# Drop stash
git stash drop stash@{0}
```

---

## Best Practices

### Do
- Pull before starting new work
- Commit often with meaningful messages
- Keep branches short-lived
- Delete merged branches
- Use `.gitignore` properly

### Don't
- Commit directly to main
- Force push shared branches
- Commit secrets or credentials
- Create giant commits
- Leave branches stale

---

## Git Configuration

### Recommended Settings

```bash
# Set default branch name
git config --global init.defaultBranch main

# Enable helpful colors
git config --global color.ui auto

# Set pull behavior
git config --global pull.rebase true

# Set push behavior
git config --global push.autoSetupRemote true
```

### Useful Aliases

```bash
git config --global alias.st status
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.cm commit
git config --global alias.lg "log --oneline --graph --all"
```

---

## Quick Reference

```bash
# Start work
git checkout main && git pull
git checkout -b feature/my-feature

# Daily workflow
git add .
git commit -m "type: description"
git push

# Update from main
git fetch origin && git rebase origin/main
git push --force-with-lease

# After merge
git checkout main && git pull
git branch -d feature/my-feature

# Undo
git reset --soft HEAD~1    # Undo commit, keep changes
git restore --staged .      # Unstage all
git stash                   # Save for later
```

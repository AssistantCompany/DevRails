# Development Glossary

> Master glossary of development terminology. Use these definitions consistently across all projects.

---

## A

### Approval
Permission to merge a PR, given by a reviewer after examining the code changes.

### Automation
Scripts or workflows that run without human intervention, like CI/CD pipelines.

---

## B

### Branch
A parallel version of the repository where changes can be made independently.

**Key Points:**
- Each branch is an isolated workspace
- Changes on one branch don't affect others
- One branch should correspond to one PR
- Common prefixes: `feature/`, `bugfix/`, `task/`, `chore/`

**Example:**
```bash
git checkout -b feature/add-login-remember-me
```

### Bug
See: [Defect](#defect)

---

## C

### CI (Continuous Integration)
Automated process that builds and tests code when changes are pushed.

**Typical CI Steps:**
1. Code pushed to branch
2. Tests run automatically
3. Linting/type checking
4. Build verification
5. Results reported on PR

### CD (Continuous Deployment)
Automated process that deploys code to production after CI passes.

### Checkout
Switching to a different branch in Git.

### Commit
A snapshot of changes saved to the repository with a message describing what changed.

**Good Commit Messages:**
- Start with type: `feat:`, `fix:`, `chore:`, `docs:`
- Describe what changed, not how
- Keep first line under 72 characters

### Conflict
See: [Merge Conflict](#merge-conflict)

---

## D

### Defect
A bug or error in existing functionality. Something that was working but is now broken, or never worked as intended.

**Key Distinction:**
- Defect = fixing broken behavior
- Feature = adding new behavior

**Examples:**
- "Login fails on Safari" (defect)
- "Password validation crashes on long input" (defect)
- "Add 'Remember Me' checkbox" (feature, not defect)

### Deploy
The process of releasing code to a server or environment (staging, production).

### Diff
The difference between two versions of code, showing what was added, removed, or changed.

---

## F

### Feature
A new capability or functionality being added to the application.

**Key Distinction:**
- Feature = something new that didn't exist before
- Defect = fixing something that should have worked

**Examples:**
- "Add dark mode toggle" (feature)
- "Implement user authentication" (feature)
- "Fix dark mode not saving preference" (defect)

### Fork
A personal copy of someone else's repository, allowing you to make changes without affecting the original.

---

## G

### Git
Distributed version control system for tracking changes in code.

### GitHub
Web-based platform for hosting Git repositories with additional features (PRs, Issues, Actions).

### GitHub Actions
CI/CD automation platform built into GitHub. Runs workflows defined in `.github/workflows/`.

---

## H

### HEAD
The current commit/branch you're working on in Git.

### Hook
A script that runs automatically at certain points in the Git workflow (pre-commit, pre-push, etc.).

---

## I

### Issue
A tracked item in GitHub Issues representing a bug, feature request, or task.

**Issue vs PR:**
- Issue = the problem or request
- PR = the code that addresses it

---

## M

### Main (Branch)
The primary branch of the repository, typically representing production-ready code. Also called `master` in older repositories.

### Merge
Combining changes from one branch into another.

**Merge Strategies:**
1. **Merge Commit**: Creates a merge commit preserving all history
2. **Squash and Merge**: Combines all commits into one (recommended)
3. **Rebase and Merge**: Replays commits on top of base branch

### Merge Conflict
When Git cannot automatically merge changes because the same lines were modified differently in both branches.

**Resolution Steps:**
1. Git marks conflicting sections
2. Developer manually resolves conflicts
3. Changes are committed
4. Merge continues

---

## P

### Pipeline
A sequence of automated steps (build, test, deploy) that code goes through.

### PR (Pull Request)
A request to merge code changes from one branch into another, including a review process.

**Critical Understanding:**
> A PR is the **container** for code changes, not the problem itself.

**PR Lifecycle:**
1. Developer creates branch
2. Developer makes changes and commits
3. Developer pushes branch to remote
4. Developer opens PR (branch → main)
5. Reviewers examine changes
6. Developer addresses feedback
7. Reviewers approve
8. PR is merged
9. Branch is deleted

**PR is NOT:**
- A bug report (that's an Issue/Defect)
- A feature request (that's an Issue)
- A task assignment (that's a ticket)

**PR IS:**
- The proposed solution to a bug
- The implementation of a feature
- The code that addresses a ticket

### Push
Uploading local commits to a remote repository.

---

## R

### Rebase
Reapplying commits on top of another base commit, creating a linear history.

**When to Use:**
- Updating your branch with latest main
- Cleaning up commit history before merge

**When NOT to Use:**
- On shared branches
- After pushing to remote (without force)

### Remote
A version of the repository hosted on a server (GitHub, GitLab, etc.).

### Repository (Repo)
A storage location for code and its entire history of changes.

### Review
The process of examining code changes before they are merged.

**Review Actions:**
- **Comment**: Ask questions or make suggestions
- **Approve**: Changes look good, ready to merge
- **Request Changes**: Changes needed before approval

### Rollback
Reverting to a previous version of code after a problematic deployment.

---

## S

### Squash
Combining multiple commits into a single commit, typically done when merging a PR.

### Staging (Environment)
A pre-production environment for testing changes before deploying to production.

### Staging (Git)
Adding changes to the "staging area" before committing them.

```bash
git add file.js    # Stage specific file
git add .          # Stage all changes
```

---

## T

### Tag
A named reference to a specific commit, often used for releases (v1.0.0, v2.1.3).

### Test
Code that verifies other code works correctly.

**Test Types:**
- **Unit Test**: Tests a single function/component
- **Integration Test**: Tests components working together
- **E2E Test**: Tests full user workflows

### Ticket
A work item in a project management system (Jira, GitHub Issues, etc.).

---

## U

### Upstream
The original repository that a fork was created from.

---

## W

### Workflow
An automated sequence of jobs defined in GitHub Actions.

### Working Directory
The local folder where you're making changes to code.

---

## Quick Reference Table

| Term | Category | One-Line Definition |
|------|----------|-------------------|
| PR | Process | Container for code changes submitted for review |
| Defect | Work Type | Bug in existing functionality |
| Feature | Work Type | New capability being added |
| Branch | Git | Isolated workspace for changes |
| Commit | Git | Snapshot of changes with a message |
| Merge | Git | Combining branches together |
| Review | Process | Examining code before approval |
| CI/CD | Automation | Build, test, and deploy automation |
| Issue | Tracking | Bug report or feature request |
| Main | Git | Primary production-ready branch |

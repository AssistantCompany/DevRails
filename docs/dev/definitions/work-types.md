# Work Types

> Understanding the different types of work helps with prioritization, estimation, and tracking.

---

## Overview

| Type | Purpose | Origin | Branch Prefix |
|------|---------|--------|---------------|
| Feature | Add new capability | Product/business intent | `feature/` |
| Defect | Fix broken behavior | Testing/users found issue | `bugfix/` |
| Task | Technical work | Infrastructure need | `task/` |
| Chore | Maintenance | Housekeeping | `chore/` |
| Spike | Research | Unknown solution | `spike/` |

---

## Feature

### Definition
New functionality that adds value to users. Something that didn't exist before.

### Characteristics
- Adds something new
- Requires design/planning
- Often has acceptance criteria
- Delivered in sprints/iterations
- Increases product capabilities

### Examples
- "Add dark mode toggle"
- "Implement user authentication"
- "Add 'Remember Me' checkbox to login"
- "Create dashboard for analytics"

### Branch Naming
```
feature/add-dark-mode
feature/user-authentication
feature/JIRA-123-remember-me
```

### Commit Prefix
```
feat: add dark mode toggle
feat: implement user authentication
```

---

## Defect (Bug)

### Definition
Something that doesn't work as intended. A problem in existing functionality.

### Characteristics
- Existing functionality is broken
- Has reproduction steps
- May be urgent (severity-based)
- Regression from previous working state
- Unintended behavior

### Severity Levels

| Severity | Description | Response |
|----------|-------------|----------|
| Critical | System down, data loss, security breach | Immediate fix required |
| High | Major feature broken, no workaround | Fix in current sprint |
| Medium | Feature degraded, workaround exists | Schedule for upcoming sprint |
| Low | Minor/cosmetic issue | Backlog |

### Examples
- "Login fails on Safari" (High)
- "Password crashes on long input" (Critical)
- "Dark mode preference doesn't save" (Medium)
- "Button alignment off by 2px" (Low)

### Branch Naming
```
bugfix/fix-safari-login
bugfix/issue-123-password-crash
bugfix/dark-mode-preference
```

### Commit Prefix
```
fix: resolve Safari login failure
fix: prevent crash on long passwords
```

---

## Task

### Definition
Technical work that doesn't directly add user-facing value but enables other work.

### Characteristics
- Infrastructure/tooling work
- Enables other development
- No direct user impact
- Often technical debt
- Developer-focused

### Examples
- "Upgrade dependencies to latest versions"
- "Add CI pipeline for automated testing"
- "Configure Docker for production"
- "Set up monitoring and alerting"

### Branch Naming
```
task/upgrade-dependencies
task/add-ci-pipeline
task/docker-production-config
```

### Commit Prefix
```
build: upgrade dependencies
ci: add automated testing pipeline
```

---

## Chore

### Definition
Maintenance and cleanup work. Housekeeping that keeps the codebase healthy.

### Characteristics
- Housekeeping tasks
- Improves code quality
- Low urgency
- Often preventive
- Keeps codebase maintainable

### Examples
- "Clean up console.log statements"
- "Update documentation"
- "Remove unused dependencies"
- "Organize file structure"

### Branch Naming
```
chore/cleanup-console-logs
chore/update-docs
chore/remove-unused-deps
```

### Commit Prefix
```
chore: remove console.log statements
docs: update API documentation
chore: remove unused dependencies
```

---

## Spike

### Definition
Research or investigation task. Time-boxed exploration when the solution is unknown.

### Characteristics
- Time-boxed research
- Produces knowledge, not code
- Informs future decisions
- Reduces uncertainty
- Often precedes features

### Examples
- "Investigate Square API rate limits"
- "Evaluate authentication libraries"
- "Research performance optimization options"
- "Explore payment gateway options"

### Branch Naming
```
spike/square-api-limits
spike/auth-library-evaluation
spike/performance-research
```

### Output
Spikes typically produce:
- Documentation of findings
- Recommendation for approach
- Proof of concept (optional)
- Decision record (ADR)

---

## Work Type to PR Relationship

Each PR should typically address **one** work item:

```
Issue (Defect)  →  PR (bugfix/issue-123)  →  Merge
Issue (Feature) →  PR (feature/new-thing) →  Merge
Ticket (Task)   →  PR (task/upgrade-deps) →  Merge
```

### Linking PRs to Issues

In PR description, use:
- `Fixes #123` - Closes the issue when PR merges
- `Closes #123` - Same as Fixes
- `Relates to #123` - Links without closing

---

## Decision Tree

```
Is something broken?
├── Yes → DEFECT
└── No
    ├── Adding new user capability?
    │   ├── Yes → FEATURE
    │   └── No
    │       ├── Technical/infrastructure work?
    │       │   ├── Yes → TASK
    │       │   └── No
    │       │       ├── Research needed?
    │       │       │   ├── Yes → SPIKE
    │       │       │   └── No → CHORE
```

---

## Commit Message Prefixes Summary

| Type | Prefix | Example |
|------|--------|---------|
| Feature | `feat:` | `feat: add user authentication` |
| Defect | `fix:` | `fix: resolve login crash` |
| Task (build) | `build:` | `build: upgrade webpack` |
| Task (CI) | `ci:` | `ci: add test workflow` |
| Chore | `chore:` | `chore: remove dead code` |
| Docs | `docs:` | `docs: update API docs` |
| Refactor | `refactor:` | `refactor: simplify auth logic` |
| Test | `test:` | `test: add login tests` |

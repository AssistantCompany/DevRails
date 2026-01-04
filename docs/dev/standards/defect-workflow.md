# Defect Workflow

> Complete guide to bug reporting, tracking, and resolution.

---

## What is a Defect?

A **defect** (or bug) is:
- Something that doesn't work as intended
- A problem in existing functionality
- Unintended behavior that needs fixing

**Defect vs Feature:**
| Defect | Feature |
|--------|---------|
| Fixes broken behavior | Adds new behavior |
| "Login crashes on Safari" | "Add 'Remember Me' option" |
| Something stopped working | Something never existed |

---

## The Defect Lifecycle

```
┌─────────────────────────────────────────────────────────────────┐
│  1. REPORT                                                      │
│     └── Bug discovered (testing, user report, monitoring)      │
│                                                                 │
│  2. DOCUMENT                                                    │
│     └── Create GitHub Issue with details                       │
│                                                                 │
│  3. TRIAGE                                                      │
│     └── Assign severity and priority                           │
│                                                                 │
│  4. INVESTIGATE                                                 │
│     └── Reproduce and find root cause                          │
│                                                                 │
│  5. BRANCH                                                      │
│     └── Create bugfix/issue-XXX-description                    │
│                                                                 │
│  6. FIX                                                         │
│     └── Implement fix + add regression test                    │
│                                                                 │
│  7. PR                                                          │
│     └── Open PR linking to issue (Fixes #XXX)                  │
│                                                                 │
│  8. REVIEW                                                      │
│     └── Code review + CI passes                                │
│                                                                 │
│  9. MERGE                                                       │
│     └── Deploy via GitHub Actions                              │
│                                                                 │
│ 10. VERIFY                                                      │
│     └── Confirm fix in production                              │
│                                                                 │
│ 11. CLOSE                                                       │
│     └── Close GitHub Issue                                     │
└─────────────────────────────────────────────────────────────────┘
```

---

## Step-by-Step Guide

### 1. Report

When a bug is discovered, report it immediately. Sources include:
- QA/testing
- User reports
- Monitoring/alerts
- Developer discovery

### 2. Document

Create a GitHub Issue with:

```markdown
## Bug Description
[Clear description of what's wrong]

## Steps to Reproduce
1. [Step 1]
2. [Step 2]
3. [Step 3]

## Expected Behavior
[What should happen]

## Actual Behavior
[What actually happens]

## Environment
- Browser: [e.g., Safari 17.0]
- OS: [e.g., macOS 14.0]
- App Version: [e.g., v2.1.3]

## Screenshots/Logs
[Attach any relevant screenshots or error logs]

## Severity
- [ ] Critical - System down, data loss
- [ ] High - Major feature broken
- [ ] Medium - Feature degraded
- [ ] Low - Minor/cosmetic
```

### 3. Triage

Assign severity based on impact:

| Severity | Description | Response Time | Example |
|----------|-------------|---------------|---------|
| Critical | System down, data loss, security | Immediate | Database corruption, auth bypass |
| High | Major feature broken, no workaround | Same day | Login fails, payments broken |
| Medium | Feature degraded, workaround exists | This sprint | Slow performance, UI glitch |
| Low | Minor/cosmetic issue | Backlog | Typo, alignment off |

Assign priority based on business impact:
- **P1**: Drop everything
- **P2**: Current sprint
- **P3**: Next sprint
- **P4**: Backlog

### 4. Investigate

Before coding:
1. **Reproduce the bug** - Confirm you can trigger it
2. **Find root cause** - Don't just fix symptoms
3. **Document findings** - Add notes to the issue
4. **Consider scope** - Does this affect other areas?

```bash
# Check logs
docker compose logs api --tail 100

# Check recent commits
git log --oneline -20

# Search for related code
grep -r "functionName" src/
```

### 5. Branch

Create a bugfix branch:

```bash
git checkout main
git pull
git checkout -b bugfix/issue-123-fix-login-crash
```

**Branch Naming:**
```
bugfix/issue-<number>-<brief-description>
bugfix/issue-123-fix-safari-login
bugfix/issue-456-prevent-null-crash
```

### 6. Fix

Implement the fix:

1. **Fix the root cause** - Not just the symptom
2. **Add regression test** - Prevent recurrence
3. **Check for similar issues** - Fix related problems

```bash
# Make fix
# Write test that would have caught this bug
npm test

# Commit
git add .
git commit -m "fix: prevent login crash on Safari

- Add null check for localStorage
- Add fallback for Safari private browsing
- Add test for localStorage unavailable

Fixes #123"
```

**Important: Add a Regression Test**
```javascript
// Test that proves the bug is fixed
test('login handles localStorage unavailable', () => {
  // Mock localStorage being unavailable
  // Verify login still works
});
```

### 7. PR

Open a Pull Request:

```markdown
## Summary
Fixes login crash on Safari when localStorage is unavailable.

## Root Cause
Safari private browsing mode throws when accessing localStorage,
causing an uncaught exception during login.

## Fix
- Added try/catch around localStorage access
- Added fallback to sessionStorage
- Added graceful degradation if both unavailable

## Test Plan
- [x] Unit tests added
- [x] Manual test on Safari private browsing
- [x] Verified on Chrome, Firefox

Fixes #123
```

**Link to Issue:**
Use `Fixes #123` in the PR description - GitHub will auto-close the issue when merged.

### 8. Review

Reviewers should check:
- [ ] Root cause is actually fixed
- [ ] Regression test is included
- [ ] No new issues introduced
- [ ] Code follows standards
- [ ] Test coverage adequate

### 9. Merge

Once approved and CI passes:
- Squash and merge (recommended)
- GitHub Actions deploys automatically

### 10. Verify

After deployment:
1. Test the fix in production
2. Monitor for errors
3. Check that issue is resolved

```bash
# Watch logs after deploy
docker compose logs api -f --tail 20
```

### 11. Close

If the issue doesn't auto-close:
1. Add comment confirming fix is deployed
2. Close the issue
3. Update any related documentation

---

## Severity Guide

### Critical
- System completely down
- Data loss or corruption
- Security vulnerability exploited
- Payment processing broken

**Response:** Immediate. All hands on deck.

### High
- Major feature broken for all users
- No workaround available
- Significant user impact

**Response:** Same day. Prioritize over other work.

### Medium
- Feature degraded but usable
- Workaround available
- Moderate user impact

**Response:** Current sprint. Plan time for fix.

### Low
- Cosmetic issues
- Minor inconvenience
- Edge cases

**Response:** Backlog. Fix when convenient.

---

## Common Patterns

### Hotfix for Production Issues

```bash
# Create hotfix branch from main
git checkout main
git pull
git checkout -b hotfix/critical-auth-fix

# Make minimal fix
# Push and create PR marked as urgent
git push -u origin hotfix/critical-auth-fix

# After merge, deploy immediately
```

### Regression After Deploy

1. **Rollback** if critical: Revert the breaking commit
2. **Forward fix** if possible: Quick patch
3. **Post-mortem**: Document what happened

```bash
# Revert a commit
git revert <commit-hash>
git push
```

---

## Best Practices

### Do
- Reproduce before fixing
- Fix root cause, not symptoms
- Add regression tests
- Link PR to issue
- Verify fix in production

### Don't
- Skip the issue - always document
- Push without testing
- Ignore related issues
- Forget the regression test
- Close without verification

---

## Quick Reference

```bash
# Investigate
docker compose logs api --tail 100
git log --oneline -20
grep -r "error" src/

# Branch
git checkout -b bugfix/issue-123-description

# Fix + Test
npm test
git add .
git commit -m "fix: description

Fixes #123"

# PR
git push -u origin bugfix/issue-123-description
# Open PR on GitHub with "Fixes #123" in description

# Verify
# After merge + deploy, test in production
```

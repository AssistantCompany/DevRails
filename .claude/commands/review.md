---
description: Review code changes against org standards checklist - correctness, tests, security, quality
allowed-tools: Bash, Read, Grep, Glob
argument-hint: [pr-number-or-empty-for-staged]
---

# Code Review

You are performing a code review following the org standards checklist.

## Arguments
PR number or empty for staged changes: $ARGUMENTS

## Steps

1. **Identify what to review**
   - If PR number provided: `gh pr diff $ARGUMENTS`
   - If empty: Review staged changes with `git diff --cached`
   - Or review uncommitted changes with `git diff`

2. **Apply review checklist**

   ### Correctness
   - [ ] Code does what it's supposed to do
   - [ ] Edge cases handled
   - [ ] Error handling appropriate
   - [ ] No obvious bugs

   ### Tests
   - [ ] New code has tests
   - [ ] Tests are meaningful (not just coverage)
   - [ ] Edge cases tested
   - [ ] Tests pass

   ### Security
   - [ ] No secrets or credentials in code
   - [ ] Input validation present
   - [ ] No SQL injection, XSS, or injection risks
   - [ ] Auth/authz properly checked

   ### Performance
   - [ ] No obvious performance issues
   - [ ] No N+1 queries
   - [ ] Appropriate caching if needed

   ### Code Quality
   - [ ] Readable and maintainable
   - [ ] Follows project conventions
   - [ ] No unnecessary complexity
   - [ ] Good naming

   ### Documentation
   - [ ] Complex logic commented
   - [ ] Public APIs documented
   - [ ] README updated if needed

3. **Provide feedback**
   - List any issues found by category
   - Suggest specific improvements
   - Acknowledge what's done well
   - Give overall assessment: Approve / Request Changes / Comment

4. **For PR reviews**
   - If reviewing a PR, offer to submit review via gh CLI
   - `gh pr review $ARGUMENTS --approve` or `--request-changes`

## Reference
Review standards: docs/dev/standards/code-review-standards.md

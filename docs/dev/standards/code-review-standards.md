# Code Review Standards

> Guidelines for reviewing code and getting your code reviewed.

---

## Why Code Review?

Code reviews:
- Catch bugs before production
- Share knowledge across team
- Maintain code quality
- Ensure consistency
- Document decisions

---

## Reviewer Checklist

### Correctness
- [ ] Does the code do what it's supposed to?
- [ ] Are edge cases handled?
- [ ] Are there any obvious bugs?
- [ ] Does it match the requirements/issue?

### Tests
- [ ] Are tests included for new code?
- [ ] Do tests cover edge cases?
- [ ] Are tests meaningful (not just for coverage)?
- [ ] Do all tests pass?

### Security
- [ ] No hardcoded secrets or credentials?
- [ ] Input validation present?
- [ ] No SQL injection or XSS vulnerabilities?
- [ ] Authentication/authorization correct?

### Performance
- [ ] No obvious performance issues?
- [ ] Database queries optimized?
- [ ] No N+1 query problems?
- [ ] Appropriate caching used?

### Code Quality
- [ ] Code is readable and maintainable?
- [ ] Follows existing patterns?
- [ ] No unnecessary complexity?
- [ ] Good naming conventions?
- [ ] Appropriate comments (where needed)?

### Documentation
- [ ] Public APIs documented?
- [ ] Complex logic explained?
- [ ] README updated if needed?

---

## How to Review

### 1. Understand Context

Before reviewing:
- Read the PR description
- Check linked issues
- Understand the goal

### 2. Review the Diff

Look at:
- Changed files
- Logic flow
- Test coverage
- Edge cases

### 3. Provide Feedback

**Types of Comments:**

| Prefix | Meaning |
|--------|---------|
| (no prefix) | Required change |
| `nit:` | Minor suggestion, optional |
| `question:` | Asking for clarification |
| `suggestion:` | Alternative approach |

**Example Comments:**

```markdown
// Required change
This will crash if `user` is null. Add a null check.

// Nit (optional)
nit: Consider renaming `x` to `userCount` for clarity.

// Question
question: Why did you choose this approach over using the existing helper?

// Suggestion
suggestion: You could simplify this with `array.filter()`.
```

### 4. Approve or Request Changes

| Action | When to Use |
|--------|-------------|
| Approve | Changes look good, ready to merge |
| Comment | Asking questions, not blocking |
| Request Changes | Issues must be fixed before merge |

---

## Being a Good Reviewer

### Do
- Be constructive and specific
- Explain **why**, not just what
- Offer solutions, not just criticism
- Praise good code
- Respond promptly
- Focus on important issues

### Don't
- Be nitpicky about style (use linters)
- Be condescending
- Demand perfection
- Block on personal preferences
- Take too long to review

### Good Feedback Examples

```markdown
✅ Good:
"This could cause a race condition if two users submit simultaneously.
Consider adding a mutex or using an atomic operation."

❌ Bad:
"This is wrong."
```

```markdown
✅ Good:
"Nice solution! One thing - this loop could be slow for large arrays.
Array.prototype.find() might be cleaner here."

❌ Bad:
"Use find() instead."
```

---

## Getting Your Code Reviewed

### Before Opening PR

1. **Self-review** your own code first
2. **Run tests** locally
3. **Check linting** passes
4. **Write a good description**
5. **Keep it focused** - one thing per PR

### PR Description Template

```markdown
## Summary
Brief description of what this PR does.

## Changes
- Added X feature
- Fixed Y bug
- Updated Z documentation

## Related Issues
Fixes #123

## Test Plan
- [ ] Unit tests pass
- [ ] Manual testing done
- [ ] Edge cases verified

## Screenshots (if UI changes)
[Before/After images]
```

### During Review

1. **Respond to all comments**
2. **Be open to feedback**
3. **Explain your reasoning** if you disagree
4. **Push fixes promptly**
5. **Re-request review** when ready

### Responding to Feedback

```markdown
✅ Good:
"Good catch! Fixed in abc123."
"I went with this approach because X, but happy to change if you prefer Y."
"Could you clarify what you mean by Z?"

❌ Bad:
"No."
"That's how I like it."
[No response]
```

---

## Review Workflow

```
1. PR Opened
   └── Author requests review

2. Review Started
   └── Reviewer examines changes

3. Feedback Given
   ├── Approve → Ready to merge
   ├── Comment → Discuss, may need changes
   └── Request Changes → Must be addressed

4. Changes Made
   └── Author pushes fixes

5. Re-review
   └── Reviewer checks fixes

6. Approved
   └── Merge when CI passes
```

---

## Time Expectations

| PR Size | Expected Review Time |
|---------|---------------------|
| Small (< 100 lines) | Same day |
| Medium (100-400 lines) | 1-2 days |
| Large (400+ lines) | Consider splitting |

**If blocked:** Ping the reviewer after 24 hours.

---

## When to Approve

Approve when:
- ✅ Code is correct
- ✅ Tests are adequate
- ✅ No security issues
- ✅ Follows standards
- ✅ Your feedback is addressed

**Don't block on:**
- Minor style preferences (let linter handle)
- "I would have done it differently" (if their approach works)
- Perfection (good enough is fine)

---

## When to Request Changes

Request changes when:
- ❌ Bug that will cause issues
- ❌ Security vulnerability
- ❌ Missing required tests
- ❌ Breaking change without migration
- ❌ Violates important standards

---

## Review Etiquette

### As Reviewer
- Review promptly (ideally same day)
- Be specific and constructive
- Distinguish nitpicks from blockers
- Acknowledge good work
- Trust the author

### As Author
- Keep PRs small and focused
- Respond to all comments
- Be open to feedback
- Don't take it personally
- Thank reviewers

---

## Quick Reference

**Reviewer:**
1. Read PR description and linked issues
2. Review code for correctness, tests, security
3. Leave constructive comments
4. Approve or request changes

**Author:**
1. Self-review before requesting review
2. Write clear PR description
3. Respond to all feedback
4. Push fixes and re-request review
5. Merge when approved and CI passes

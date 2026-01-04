# Commit Message Template

> Guidelines for writing clear, consistent commit messages.

## Format

```
<type>: <short description>

[optional body]

[optional footer]
```

## Types

| Type | Use For | Example |
|------|---------|---------|
| `feat` | New feature | `feat: add dark mode toggle` |
| `fix` | Bug fix | `fix: resolve login crash` |
| `docs` | Documentation | `docs: update API reference` |
| `style` | Formatting only | `style: fix indentation` |
| `refactor` | Code restructure | `refactor: simplify auth flow` |
| `test` | Adding tests | `test: add login unit tests` |
| `chore` | Maintenance | `chore: update dependencies` |
| `build` | Build system | `build: upgrade webpack` |
| `ci` | CI/CD changes | `ci: add deploy workflow` |
| `perf` | Performance | `perf: optimize database query` |

## Rules

1. **First line ≤ 72 characters**
2. **Use imperative mood**: "Add" not "Added"
3. **No period at end of first line**
4. **Separate body with blank line**
5. **Body explains why, not what**

## Examples

### Simple
```
feat: add user authentication
```

### With Body
```
fix: prevent crash on empty input

The input field was not validating for empty strings,
causing a null reference exception when submitted.

Added null check and user-friendly error message.
```

### With Issue Reference
```
fix: resolve Safari login issue

Added null check for localStorage in Safari private mode.

Fixes #123
```

### Breaking Change
```
feat!: change API response format

BREAKING CHANGE: The /users endpoint now returns an object
instead of an array. Update client code accordingly.
```

## Quick Reference

```bash
# Feature
git commit -m "feat: add dark mode"

# Bug fix
git commit -m "fix: prevent null pointer"

# With body
git commit -m "fix: handle edge case

Added validation for empty strings."

# With issue
git commit -m "fix: login crash

Fixes #123"
```

---
description: Help format a conventional commit message with proper type, scope, and description
allowed-tools: Bash, Read
argument-hint: [commit-message-or-empty]
---

# Conventional Commit Helper

You are helping format a commit message following conventional commits.

## Arguments
Optional message: $ARGUMENTS

## Steps

1. **Check staged changes**
   - Run `git status` to see what's staged
   - Run `git diff --cached --stat` to see staged file summary
   - If nothing staged, suggest what to stage

2. **Determine commit type**
   Based on the changes, select the appropriate type:
   - `feat:` - New feature or capability
   - `fix:` - Bug fix
   - `docs:` - Documentation only
   - `style:` - Formatting, no code change
   - `refactor:` - Code restructuring, no behavior change
   - `test:` - Adding or updating tests
   - `chore:` - Maintenance, dependencies, config

3. **Format the message**
   ```
   <type>: <short description (50 chars max)>

   <optional body explaining WHY, not WHAT>

   <optional footer: Fixes #123, Breaking Change, etc>
   ```

4. **If user provided message**
   - Parse their intent from $ARGUMENTS
   - Reformat to conventional commit style
   - Suggest the properly formatted version

5. **Execute commit**
   - Show the formatted message
   - Ask for confirmation
   - Run: `git commit -m "<formatted-message>"`

## Examples

**Input:** "fixed the login bug"
**Output:**
```
fix: resolve login authentication failure

Corrected null check in auth middleware that caused
login to fail for users with empty session tokens.
```

**Input:** "added dark mode"
**Output:**
```
feat: add dark mode theme support

Implemented theme toggle in settings with
localStorage persistence.
```

## Reference
Commit format: docs/dev/templates/commit-message-template.md
Git workflow: docs/dev/standards/git-workflow.md

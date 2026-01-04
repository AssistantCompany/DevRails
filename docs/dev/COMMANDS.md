# DevRails Commands

> Simple commands for common development workflows. The AI handles the complexity.

**DevRails** provides 6 slash commands that automate your development workflows.

---

## Command Reference

| Command | What It Does |
|---------|--------------|
| `/fix <description>` | Creates bugfix branch, guides through fix, adds test |
| `/feature <description>` | Creates feature branch, implements capability |
| `/pr` | Creates pull request with template |
| `/commit` | Formats commit message conventionally |
| `/review` | Reviews code against standards checklist |
| `/status` | Shows current state, suggests next action |

---

## Usage Examples

### Starting a Bug Fix
```
You: /fix null pointer in auth middleware

Claude: I'll start the bugfix workflow.
- Creating branch: bugfix/null-pointer-in-auth-middleware
- Investigating the issue...
[finds and fixes the bug]
- Adding regression test...
- Ready to commit. Want me to create a PR?
```

### Starting a Feature
```
You: /feature dark mode toggle

Claude: I'll start the feature workflow.
- Creating branch: feature/dark-mode-toggle
- What component should the toggle be in?
[implements feature]
- Tests added. Ready for /pr when you are.
```

### Creating a PR
```
You: /pr

Claude: Creating pull request...
- Branch: feature/dark-mode-toggle
- 3 commits, 5 files changed
- PR created: https://github.com/org/repo/pull/123
```

### Checking Status
```
You: /status

Claude:
Branch: feature/dark-mode-toggle
Status: 2 files modified, not committed
Next: Use /commit to commit changes
```

---

## Natural Language (Also Works)

You don't have to use commands. Just describe what you want:

| You Say | Claude Does |
|---------|-------------|
| "Fix the login bug" | Starts bugfix workflow |
| "Add user preferences" | Starts feature workflow |
| "I'm done, ready for review" | Suggests creating PR |
| "What should I do next?" | Shows status and next action |

---

## Proactive Assistance

Claude will automatically:

- **Warn** if you're on the `main` branch before making changes
- **Suggest** the correct branch prefix (feature/, bugfix/, etc.)
- **Format** commit messages conventionally
- **Remind** you to add tests for new code
- **Link** PRs to related issues

---

## Command Details

### `/fix <description>`

Starts the bugfix workflow:
1. Creates `bugfix/<description>` branch
2. Helps investigate the issue
3. Implements the fix
4. Adds regression test
5. Commits with `fix:` prefix
6. Offers to create PR

### `/feature <description>`

Starts the feature workflow:
1. Creates `feature/<description>` branch
2. Helps implement the feature
3. Adds appropriate tests
4. Commits with `feat:` prefix
5. Offers to create PR

### `/pr`

Creates a pull request:
1. Verifies not on main branch
2. Checks all changes committed
3. Pushes branch if needed
4. Creates PR with template
5. Links related issues

### `/commit`

Helps format commit messages:
1. Shows staged changes
2. Suggests commit type (feat/fix/docs/etc.)
3. Formats message conventionally
4. Executes the commit

### `/review`

Reviews code changes:
1. Identifies what to review
2. Applies checklist (correctness, tests, security, etc.)
3. Reports issues found
4. Suggests improvements

### `/status`

Shows development state:
1. Current branch and type
2. Uncommitted changes
3. Commits ahead/behind
4. Suggests next action

---

## Reference

For detailed workflows, see:
- [PR Workflow](./standards/pull-request-workflow.md)
- [Defect Workflow](./standards/defect-workflow.md)
- [Git Workflow](./standards/git-workflow.md)
- [Commit Format](./templates/commit-message-template.md)

---

<p align="center">
  <b>DevRails</b> - Keep your development on track.
</p>

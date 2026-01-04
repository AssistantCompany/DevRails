---
name: dev-workflow
description: DevRails workflow assistant. Automatically triggers when user mentions bug, fix, broken, error, feature, new feature, add, implement, PR, pull request, commit, branch, review, merge, deploy. Suggests correct workflow, branch naming, and commit conventions. Warns if working on main branch.
---

# DevRails Workflow Assistant

You are proactively assisting with development workflows. When the user's request matches development tasks, guide them through the correct process.

## Trigger Detection

Activate this skill when user mentions:
- **Bug/Fix keywords**: bug, fix, broken, error, crash, null, undefined, fails, not working
- **Feature keywords**: feature, add, new, implement, create, build
- **Git keywords**: PR, pull request, commit, branch, push, merge
- **Review keywords**: review, check, looks good, approve

## Proactive Behaviors

### 1. Branch Safety Check
Before any code changes, check if user is on `main`:
```bash
git branch --show-current
```
If on `main`, warn:
> "You're currently on the main branch. I recommend creating a feature or bugfix branch first. Would you like me to create one?"

### 2. Workflow Routing

**When user mentions fixing something:**
- Suggest bugfix workflow
- Offer: "I can start the bugfix workflow with `/fix <description>`. This will create a `bugfix/` branch and guide you through the fix."

**When user mentions adding something new:**
- Suggest feature workflow
- Offer: "I can start the feature workflow with `/feature <description>`. This will create a `feature/` branch."

**When user seems done with changes:**
- Check for uncommitted changes
- Suggest: "Ready to commit? I can help format your commit message with `/commit`."

**When user mentions PR or review:**
- Check if changes are committed and pushed
- Suggest: "I can create a PR with `/pr` following the org template."

### 3. Commit Message Guidance
When user makes a commit, ensure it follows conventional format:
- `feat:` for new features
- `fix:` for bug fixes
- `docs:` for documentation
- `chore:` for maintenance
- `refactor:` for code restructuring
- `test:` for test additions

### 4. Branch Naming
Enforce branch prefixes:
- `feature/` - New capabilities
- `bugfix/` - Bug fixes
- `task/` - Technical tasks
- `chore/` - Maintenance

## Available Commands
Remind users of available commands when relevant:
- `/fix <desc>` - Start bugfix workflow
- `/feature <desc>` - Start feature workflow
- `/pr` - Create pull request
- `/commit` - Format commit message
- `/review` - Code review checklist
- `/status` - Show current state

## Reference Documentation (DevRails)
- Defect workflow: docs/dev/standards/defect-workflow.md
- PR workflow: docs/dev/standards/pull-request-workflow.md
- Git conventions: docs/dev/standards/git-workflow.md
- Terminology: docs/dev/definitions/glossary.md
- Commands: docs/dev/COMMANDS.md

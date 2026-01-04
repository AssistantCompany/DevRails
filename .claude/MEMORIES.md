# DevRails - AI Memory

> Persistent instructions for AI coding assistants.
> Master copy: `../docs/dev/MEMORIES.md`

**DevRails** keeps your development on track with consistent workflows and conventions.

---

## Always Do

### Before Starting Work
- Check org standards at `../docs/dev/` before starting any work
- Read the [glossary](../docs/dev/definitions/glossary.md) to ensure consistent terminology
- Identify the work type: defect, feature, task, or chore

### For Code Changes
- Follow the [PR workflow](../docs/dev/standards/pull-request-workflow.md) for all code changes
- One branch = one PR = one unit of work
- Use branch naming conventions: `feature/`, `bugfix/`, `task/`, `chore/`

### For Bug Fixes
- Follow the [defect workflow](../docs/dev/standards/defect-workflow.md)
- Create GitHub Issue first if not exists
- Link PR to issue with `Fixes #123`
- Add regression test

### For New Projects (Greenfield)
- Create CLAUDE.md using [template](../docs/dev/templates/project-claude-md.template)
- Customize with project-specific details
- Follow org standards for all workflows

### For Existing Projects (Brownfield)
- **Never replace existing files** - merge instead
- If CLAUDE.md exists → ADD breadcrumb section, keep existing content
- If .github/ templates exist → Keep them, don't override
- Use [BREADCRUMB_TEMPLATE.md](../docs/dev/BREADCRUMB_TEMPLATE.md) for the section to add

---

## Terminology

Use these terms consistently (see [glossary](../docs/dev/definitions/glossary.md) for full definitions):

| Term | Meaning |
|------|---------|
| PR | Pull Request - container for code changes, not the problem |
| Defect | Bug - something broken that was working before |
| Feature | New capability - something that didn't exist before |
| Branch | Workspace for changes - one branch per PR |
| Review | Code examination before merge |

---

## Workflow Quick Reference

### PR Lifecycle
1. Create branch from main
2. Make changes + commit
3. Push to remote
4. Open PR (branch → main)
5. Address review feedback
6. Merge when approved + CI passes
7. Delete branch

### Defect Lifecycle
1. Report → GitHub Issue
2. Triage → Assign severity
3. Branch → `bugfix/issue-123-description`
4. Fix → Include regression test
5. PR → Link to issue
6. Review → Code review + CI
7. Merge → Deploy
8. Verify → Confirm in production
9. Close → Close GitHub Issue

---

## Proactive Workflow Guidance

### Before Any Code Changes
- Always check current branch with `git branch --show-current`
- If on `main`, warn user and suggest creating appropriate branch first
- Offer to start workflow with `/fix` or `/feature` command

### Suggest Commands When Relevant
When user mentions development tasks, offer the appropriate command:
- "bug", "fix", "broken", "error" → Suggest `/fix <description>`
- "feature", "add", "new", "implement" → Suggest `/feature <description>`
- "done", "finished", "ready" → Suggest `/pr` or `/commit`
- "review", "check" → Suggest `/review`
- "what next", "status" → Use `/status`

### Available Commands
| Command | Purpose |
|---------|---------|
| `/fix <desc>` | Start bugfix workflow |
| `/feature <desc>` | Start feature workflow |
| `/pr` | Create pull request |
| `/commit` | Format commit message |
| `/review` | Code review checklist |
| `/status` | Show state, suggest next |

### Commit Conventions
Always use conventional commit format:
- `feat:` - New feature
- `fix:` - Bug fix
- `docs:` - Documentation
- `chore:` - Maintenance
- `refactor:` - Code restructure
- `test:` - Tests

---

## Project Integration Checklist

When working on any project:

- [ ] CLAUDE.md exists in project root (create if missing, merge if exists)
- [ ] CLAUDE.md has breadcrumb to org standards
- [ ] **Did NOT override** existing project content
- [ ] Using consistent terminology from glossary
- [ ] Following appropriate workflow (PR or defect)
- [ ] Using templates for PRs and issues (unless project has its own)

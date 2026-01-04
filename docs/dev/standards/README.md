# Standards

> How we work. Workflows, conventions, and best practices.

## Files

| File | Description |
|------|-------------|
| [pull-request-workflow.md](./pull-request-workflow.md) | Complete PR lifecycle from branch to merge |
| [defect-workflow.md](./defect-workflow.md) | Bug reporting through resolution |
| [git-workflow.md](./git-workflow.md) | Branch strategy and commit conventions |
| [github-actions-standards.md](./github-actions-standards.md) | CI/CD patterns using GitHub Actions |
| [code-review-standards.md](./code-review-standards.md) | Code review checklist and process |
| [ai-development-guide.md](./ai-development-guide.md) | Guidelines for AI-assisted development |

## Quick Reference

### For Code Changes
1. Create branch → [git-workflow.md](./git-workflow.md)
2. Make changes and commit
3. Open PR → [pull-request-workflow.md](./pull-request-workflow.md)
4. Review → [code-review-standards.md](./code-review-standards.md)
5. Merge when approved

### For Bug Fixes
1. Report issue → [defect-workflow.md](./defect-workflow.md)
2. Triage and assign
3. Create bugfix branch
4. Fix + add test
5. Open PR linking to issue
6. Review and merge
7. Verify in production

### For AI Developers
Start with [ai-development-guide.md](./ai-development-guide.md), then follow the appropriate workflow.

## Core Principles

1. **One branch = one PR = one unit of work**
2. **Tests are required** for all code changes
3. **Review before merge** - no direct commits to main
4. **Link PRs to issues** when addressing bugs or features
5. **Keep PRs focused** - smaller PRs are easier to review

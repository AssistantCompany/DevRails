# Templates

> Reusable templates for PRs, issues, commits, and project setup.

## Available Templates

| Template | Purpose | Copy To |
|----------|---------|---------|
| [org-claude-md.template](./org-claude-md.template) | Org-level CLAUDE.md | `<ORG_ROOT>/CLAUDE.md` |
| [project-claude-md.template](./project-claude-md.template) | Project CLAUDE.md | `projects/<name>/CLAUDE.md` |
| [pull-request-template.md](./pull-request-template.md) | PR descriptions | `.github/pull_request_template.md` |
| [bug-report-template.md](./bug-report-template.md) | Bug reports | `.github/ISSUE_TEMPLATE/bug_report.md` |
| [feature-request-template.md](./feature-request-template.md) | Feature requests | `.github/ISSUE_TEMPLATE/feature_request.md` |
| [commit-message-template.md](./commit-message-template.md) | Commit messages | Reference only |

---

## Usage

### GitHub Templates

To enable GitHub to use these templates automatically:

1. **PR Template:**
   ```bash
   mkdir -p .github
   cp docs/dev/templates/pull-request-template.md .github/pull_request_template.md
   ```

2. **Issue Templates:**
   ```bash
   mkdir -p .github/ISSUE_TEMPLATE
   cp docs/dev/templates/bug-report-template.md .github/ISSUE_TEMPLATE/bug_report.md
   cp docs/dev/templates/feature-request-template.md .github/ISSUE_TEMPLATE/feature_request.md
   ```

### Org Setup (New Server)

```bash
# Copy org-level template
cp docs/dev/templates/org-claude-md.template CLAUDE.md
# Edit to customize for your organization
```

### Project Setup

When creating a new project:
```bash
cp docs/dev/templates/project-claude-md.template projects/my-project/CLAUDE.md
# Edit to add project-specific details
```

---

## Customization

These templates are starting points. Customize for your project:

1. Copy template to destination
2. Edit to add project-specific sections
3. Remove sections that don't apply
4. Keep breadcrumb to org standards

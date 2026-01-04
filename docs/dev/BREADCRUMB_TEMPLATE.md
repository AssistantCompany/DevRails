# DevRails Breadcrumb Template

> **ADD** this section to project CLAUDE.md files to link to DevRails standards.
> This is for **merging into existing files**, not replacing them.

## Important: Merge, Don't Replace

- If project has existing CLAUDE.md → **ADD** this section, keep existing content
- If project has no CLAUDE.md → Use `project-claude-md.template` instead

---

## Template (Copy Below This Line)

```markdown
## Organization Standards (DevRails)

This project follows DevRails development standards.

### Quick Links
- [DevRails](../../docs/dev/README.md) - Main documentation
- [Commands](../../docs/dev/COMMANDS.md) - /fix, /feature, /pr, /commit, /review, /status
- [Glossary](../../docs/dev/definitions/glossary.md) - Terminology definitions
- [PR Workflow](../../docs/dev/standards/pull-request-workflow.md) - How to create PRs
- [Defect Workflow](../../docs/dev/standards/defect-workflow.md) - How to fix bugs

### Key Principles
- One branch = one PR = one unit of work
- PR is the container for changes, not the problem itself
- Use DevRails commands for consistent workflows
- Use consistent terminology from the glossary
```

---

## Usage

### For Projects in `projects/` Directory

The template above uses `../../docs/dev/` which works for projects located at:
```
<ORG_ROOT>/projects/project-name/CLAUDE.md
```

### For Projects at Different Depths

Adjust the relative path based on your project location:

| Project Location | Path to docs/dev/ |
|-----------------|-------------------|
| `projects/project-name/` | `../../docs/dev/` |
| `projects/group/project-name/` | `../../../docs/dev/` |
| Root level project | `./docs/dev/` |

---

## Minimal Version

If you need a shorter version:

```markdown
## Organization Standards (DevRails)

This project follows [DevRails](../../docs/dev/README.md) development standards.

Commands: /fix, /feature, /pr, /commit, /review, /status

Key docs:
- [Commands](../../docs/dev/COMMANDS.md)
- [PR Workflow](../../docs/dev/standards/pull-request-workflow.md)
- [Defect Workflow](../../docs/dev/standards/defect-workflow.md)
```

---

## Verification

After adding the breadcrumb, verify:
- [ ] Links resolve correctly (relative paths are right)
- [ ] Section is visible in CLAUDE.md
- [ ] AI can navigate to standards from project

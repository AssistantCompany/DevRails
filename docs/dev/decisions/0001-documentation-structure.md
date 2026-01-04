# ADR-0001: DevRails Documentation Structure

## Status

**Accepted**

## Date

2026-01-04

## Context

Organizations with multiple projects need consistent development practices. Common issues:

1. **Inconsistent terminology** - Different terms used for the same concepts
2. **No shared standards** - Each project developed its own conventions
3. **AI developer confusion** - Claude Code lacked consistent guidance
4. **Onboarding friction** - New projects required reinventing processes

Requirements:
- Standards must be **shared** across all projects
- Package must be **portable** to new servers
- AI developers must **automatically** follow standards
- Documentation must be **easy to maintain**

## Decision

Create **DevRails** - a centralized development standards package at `docs/dev/` with:

### Structure
```
docs/dev/
├── README.md              # Navigation hub
├── SETUP.md               # New server installation
├── MEMORIES.md            # AI persistent instructions
├── BREADCRUMB_TEMPLATE.md # Project integration template
├── standards/             # Workflows and processes
├── definitions/           # Glossary and terminology
├── templates/             # Reusable templates
└── decisions/             # ADRs (this directory)
```

### Integration Strategy
1. **Org-level CLAUDE.md** - Points AI to standards first
2. **Project CLAUDE.md breadcrumbs** - Link back to org standards
3. **AI memories** - Persistent instructions in `.claude/`
4. **Relative paths** - No hardcoded server paths

### Key Design Decisions
1. **Location: `docs/dev/`** - Inside existing docs folder, not separate
2. **Relative paths only** - Enables portability
3. **AI-first documentation** - Designed for both humans and AI
4. **Breadcrumb pattern** - Projects reference org, not duplicate

## Consequences

### Positive
- **Consistency** - All projects follow same standards
- **Portability** - Package can be installed on any server
- **AI integration** - Claude Code automatically follows standards
- **Maintainability** - Single source of truth for updates
- **Onboarding** - New projects get standards automatically

### Negative
- **Initial effort** - Requires creating comprehensive documentation
- **Migration work** - Existing projects need breadcrumb updates
- **Learning curve** - Team needs to learn where standards live
- **Maintenance overhead** - Standards must be kept current

### Neutral
- **GitHub-specific** - Templates designed for GitHub (not GitLab, etc.)
- **Claude Code focus** - AI instructions specific to Claude Code

## Alternatives Considered

### Alternative 1: Per-Project Standards
Each project maintains its own complete standards.

**Rejected because:**
- Duplication across projects
- Standards drift over time
- Harder to update consistently
- More maintenance overhead

### Alternative 2: Separate Repository
Standards in a dedicated `dev-standards` repository.

**Rejected because:**
- Requires cloning additional repo
- Harder to keep in sync
- Cross-repo references are complex
- Adds deployment complexity

### Alternative 3: Wiki-Based
Standards in GitHub Wiki or Notion.

**Rejected because:**
- Not version controlled with code
- Harder for AI to access
- Separate from development flow
- Risk of becoming stale

## Related

- [Microsoft Engineering Fundamentals Playbook](https://microsoft.github.io/code-with-engineering-playbook/)
- [ADR GitHub Organization](https://adr.github.io/)
- [Write the Docs](https://www.writethedocs.org/guide/index.html)

---

## Notes

This ADR documents the initial creation of DevRails. Future ADRs should be created for significant changes to the structure or processes.

---

<p align="center">
  <b>DevRails</b> - Keep your development on track.
</p>

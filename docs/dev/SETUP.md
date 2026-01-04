# DevRails Setup Guide

> How to install DevRails on a new server or integrate with existing projects.

---

## Prerequisites

### Required

| Requirement | Description |
|-------------|-------------|
| **Git** | Version control (any recent version) |
| **AI Coding Assistant** | Claude Code, OpenAI Codex, Cursor, or similar |
| **GitHub Account** | For PR/issue integration (or GitLab/Bitbucket) |

### Supported AI Assistants

| Assistant | Support Level | Notes |
|-----------|---------------|-------|
| **Claude Code** | Full | Primary target - commands and skills work natively |
| **OpenAI Codex** | Full | Reads standards and follows workflows |
| **Cursor** | Full | Works with .cursor rules integration |
| **GitHub Copilot Chat** | Partial | May need manual command invocation |
| **Other AI Assistants** | Varies | Any assistant that reads markdown docs |

### Optional

- Node.js/npm (for JavaScript/TypeScript projects)
- GitHub CLI (`gh`) for PR automation
- Docker (for containerized workflows)

---

## Greenfield vs Brownfield

DevRails handles both scenarios:

| Scenario | Description | Approach |
|----------|-------------|----------|
| **Greenfield** | New server, no existing files | Use templates directly |
| **Brownfield** | Existing projects with files | **Merge**, don't replace |

### Key Principle: Never Override Existing Content

- **Existing CLAUDE.md** → ADD breadcrumb section, keep all existing content
- **Existing .github/ templates** → Keep yours, use DevRails templates as reference
- **Existing README.md** → Keep yours, optionally add standards link
- **docs/dev/** → Safe to copy (new directory)

---

## Installation Steps

### Step 1: Copy DevRails Package

```bash
# Option A: Clone from GitHub
git clone https://github.com/YOUR_ORG/devrails.git
cp -r devrails/docs/dev /path/to/your/org/docs/dev
cp -r devrails/.claude /path/to/your/org/.claude

# Option B: Copy from existing installation
cp -r <SOURCE>/docs/dev/* docs/dev/
cp -r <SOURCE>/.claude/* .claude/
```

### Step 2: Setup Org-Level CLAUDE.md

#### If NO existing CLAUDE.md (Greenfield):
```bash
cp docs/dev/templates/org-claude-md.template CLAUDE.md
```
Then customize with your org name and projects.

#### If CLAUDE.md already exists (Brownfield):
**Do NOT replace it.** Instead, add this section at the top:

```markdown
## Organization Standards (DevRails)

Before working on any project, review:
- Development standards: ./docs/dev/
- Commands: ./docs/dev/COMMANDS.md
- Glossary: ./docs/dev/definitions/glossary.md

Available commands: /fix, /feature, /pr, /commit, /review, /status
```

Keep all your existing content below the new section.

### Step 3: Setup AI Memory and Commands

```bash
# Create .claude directory if it doesn't exist
mkdir -p .claude

# Copy memories (required)
cp docs/dev/MEMORIES.md .claude/MEMORIES.md

# Copy commands (required for slash commands)
cp -r <SOURCE>/.claude/commands .claude/commands

# Copy skills (required for proactive suggestions)
cp -r <SOURCE>/.claude/skills .claude/skills
```

### Step 4: Integrate Existing Projects

For each project in your organization:

#### If NO CLAUDE.md exists (Greenfield project):
```bash
cp docs/dev/templates/project-claude-md.template projects/<name>/CLAUDE.md
```
Then customize with project-specific build commands, architecture, etc.

#### If CLAUDE.md already exists (Brownfield project):
**Do NOT replace it.** Add the breadcrumb section from `BREADCRUMB_TEMPLATE.md`:

1. Open the existing `CLAUDE.md`
2. Add the "Organization Standards" section near the top
3. Keep all existing project-specific content

Example merge:
```markdown
# CLAUDE.md (existing title)

## Organization Standards (DevRails)    <-- ADD THIS SECTION
This project follows DevRails development standards.
See: ../../docs/dev/README.md

Commands: /fix, /feature, /pr, /commit, /review, /status

## Build Commands                       <-- KEEP EXISTING CONTENT
[existing project content...]
```

### Step 5: Verify Installation

```bash
# Run from org root
echo "=== DevRails Verification ===" && \
ls docs/dev/README.md && echo "OK: docs/dev/ exists" && \
ls CLAUDE.md && echo "OK: Org CLAUDE.md exists" && \
ls .claude/MEMORIES.md && echo "OK: AI memories exist" && \
ls .claude/commands/fix.md && echo "OK: Commands exist" && \
ls .claude/skills/dev-workflow/SKILL.md && echo "OK: Skills exist" && \
echo "=== DevRails Ready ==="
```

**Checklist:**
- [ ] `docs/dev/README.md` exists
- [ ] `CLAUDE.md` exists at org root
- [ ] `.claude/MEMORIES.md` exists
- [ ] `.claude/commands/` contains command files
- [ ] `.claude/skills/dev-workflow/` exists
- [ ] Each project has CLAUDE.md with breadcrumb

---

## Directory Structure After Installation

```
<ORG_ROOT>/
├── CLAUDE.md                    # Org-level AI instructions
├── .claude/
│   ├── MEMORIES.md              # AI persistent memory
│   ├── commands/                # Slash commands
│   │   ├── fix.md
│   │   ├── feature.md
│   │   ├── pr.md
│   │   ├── commit.md
│   │   ├── review.md
│   │   └── status.md
│   └── skills/                  # Proactive AI skills
│       └── dev-workflow/
│           ├── SKILL.md
│           └── workflows.md
├── docs/
│   └── dev/                     # DevRails standards package
│       ├── README.md
│       ├── COMMANDS.md
│       ├── SETUP.md
│       ├── MEMORIES.md
│       ├── standards/
│       ├── definitions/
│       ├── templates/
│       └── decisions/
└── projects/
    ├── project-a/
    │   └── CLAUDE.md            # With breadcrumb to DevRails
    └── project-b/
        └── CLAUDE.md            # With breadcrumb to DevRails
```

---

## Testing Your Installation

After installation, test the commands:

```
# In your AI assistant, try:
/status                    # Should show current git state
/fix test-installation     # Should create bugfix branch
git checkout main          # Go back to main
git branch -D bugfix/test-installation  # Clean up
```

---

## Updating DevRails

When updating to a new version:

1. Pull/copy new `docs/dev/` content
2. Pull/copy new `.claude/commands/` and `.claude/skills/`
3. Update `.claude/MEMORIES.md` if changed
4. Project breadcrumbs don't need updating (they reference by path)

---

## Troubleshooting

### Commands not recognized
- Verify `.claude/commands/` directory exists
- Check command files have `.md` extension
- Restart your AI assistant session

### AI not following standards
- Verify org-level CLAUDE.md exists
- Check `.claude/MEMORIES.md` is present
- Ensure project CLAUDE.md has breadcrumb section

### Proactive suggestions not working
- Verify `.claude/skills/dev-workflow/SKILL.md` exists
- Check skill description matches trigger keywords
- Some AI assistants may not support skills

### Standards not found
- Check relative paths in breadcrumb
- Standard pattern: `../../docs/dev/` from `projects/project-name/`
- Adjust depth for nested project structures

---

## Uninstalling

To remove DevRails:

```bash
rm -rf docs/dev/
rm -rf .claude/commands/
rm -rf .claude/skills/
rm .claude/MEMORIES.md
# Manually remove breadcrumb sections from CLAUDE.md files
```

---

<p align="center">
  <b>DevRails</b> - Keep your development on track.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/DevRails-Keep%20Development%20On%20Track-blue?style=for-the-badge" alt="DevRails">
</p>

<h1 align="center">DevRails</h1>

<p align="center">
  <b>Keep your development on track.</b><br>
  A portable, AI-first development standards package that automates workflows and keeps teams consistent.
</p>

<p align="center">
  <a href="#quick-start"><img src="https://img.shields.io/badge/Setup-5%20minutes-brightgreen?style=flat-square" alt="Setup Time"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square" alt="License: MIT"></a>
  <a href="#compatibility"><img src="https://img.shields.io/badge/AI-Powered-purple?style=flat-square" alt="AI-Powered"></a>
  <a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-Welcome-brightgreen?style=flat-square" alt="PRs Welcome"></a>
</p>

<p align="center">
  <a href="#the-problem">Problem</a> •
  <a href="#the-solution">Solution</a> •
  <a href="#quick-start">Quick Start</a> •
  <a href="#commands">Commands</a> •
  <a href="#compatibility">Compatibility</a>
</p>

---

## The Problem

```
Developer: "How do I fix a bug here?"
Team Lead:  "Read the wiki, check the PR template, use conventional commits,
             don't forget to link the issue, add a test..."
Developer:  *spends 30 minutes figuring it out*
```

## The Solution

```
Developer: /fix login authentication error

DevRails:  Creating bugfix/login-authentication-error branch...
           [fixes issue, adds test, commits properly]
           Ready for PR. Run /pr to create it.
```

**One command. Done.**

---

## What is DevRails?

**DevRails** is a drop-in development standards package that works with AI coding assistants to automate your workflows.

- **You say:** `/fix login bug`
- **AI does:** Creates branch, investigates, fixes, adds test, commits properly, offers to create PR

No documentation to read. No conventions to memorize. The AI knows what to do.

---

## Quick Start

### Prerequisites

| Requirement | Why |
|-------------|-----|
| **Git** | Version control |
| **AI Coding Assistant** | Claude Code, OpenAI Codex, Cursor, or similar |
| **GitHub/GitLab** | For PR integration |

### Step 1: Clone DevRails (You do this)

```bash
git clone https://github.com/AssistantCompany/DevRails.git
cd DevRails
```

### Step 2: Copy to Your Organization (You do this)

```bash
# Copy docs/dev/ to your org root
cp -r docs/dev /path/to/your/org/docs/dev

# Copy .claude/ to your org root
cp -r .claude /path/to/your/org/.claude
```

### Step 3: Create Org CLAUDE.md (You do this)

Create a `CLAUDE.md` file at your org root:

```bash
cp docs/dev/templates/org-claude-md.template /path/to/your/org/CLAUDE.md
```

Edit it with your org name and project list.

### Step 4: Start Using Commands (AI does the work)

Open your AI coding assistant in any project and use:

```
/status                    # AI shows current state
/fix <bug description>     # AI creates branch, fixes bug, adds test
/feature <description>     # AI creates branch, implements feature
/pr                        # AI creates pull request
```

**That's it. You're on track.**

---

## Commands

| Command | What You Say | What AI Does |
|---------|--------------|--------------|
| `/fix <description>` | "Fix the login bug" | Creates `bugfix/` branch, investigates, fixes, adds regression test, commits with `fix:` prefix |
| `/feature <description>` | "Add dark mode" | Creates `feature/` branch, implements, adds tests, commits with `feat:` prefix |
| `/pr` | "Create a PR" | Pushes branch, creates PR with template, links issues |
| `/commit` | "Commit this" | Formats message with conventional commit style |
| `/review` | "Review this code" | Checks security, tests, quality, performance |
| `/status` | "Where am I?" | Shows branch, changes, suggests next action |

### Natural Language Works Too

You don't need to use commands. Just describe what you want:

| You Say | AI Does |
|---------|---------|
| "Fix the authentication bug" | Starts bugfix workflow |
| "Add user settings page" | Starts feature workflow |
| "I'm done with this" | Suggests creating PR |
| "What should I do next?" | Shows status and suggests action |

---

## What You Do vs What AI Does

### Starting a Bug Fix

| Step | Who | Action |
|------|-----|--------|
| 1 | **You** | Say: `/fix null pointer in auth` |
| 2 | **AI** | Creates `bugfix/null-pointer-in-auth` branch |
| 3 | **AI** | Searches code, identifies root cause |
| 4 | **AI** | Implements fix |
| 5 | **AI** | Adds regression test |
| 6 | **AI** | Commits with `fix: resolve null pointer in auth` |
| 7 | **AI** | Asks: "Ready for PR?" |
| 8 | **You** | Say: "Yes" or `/pr` |
| 9 | **AI** | Creates PR with template, links issues |

### Starting a Feature

| Step | Who | Action |
|------|-----|--------|
| 1 | **You** | Say: `/feature dark mode toggle` |
| 2 | **AI** | Creates `feature/dark-mode-toggle` branch |
| 3 | **AI** | Asks clarifying questions if needed |
| 4 | **AI** | Implements feature following existing patterns |
| 5 | **AI** | Adds tests |
| 6 | **AI** | Commits with `feat: add dark mode toggle` |
| 7 | **AI** | Asks: "Ready for PR?" |

### Proactive Behavior

The AI will automatically:

- **Warn** if you're on `main` branch before making changes
- **Suggest** correct branch prefix (`feature/`, `bugfix/`, etc.)
- **Format** commit messages conventionally
- **Remind** you to add tests
- **Link** PRs to related issues

---

## Compatibility

### Supported AI Assistants

| Assistant | Status | Notes |
|-----------|--------|-------|
| **Claude Code** | ✅ Full Support | Primary target - commands and proactive skills work natively |
| **OpenAI Codex** | ✅ Compatible | Reads standards, follows workflows |
| **Cursor** | ✅ Compatible | Works with custom rules |
| **GitHub Copilot Chat** | ⚡ Partial | May need manual command invocation |
| **Other AI Assistants** | ⚡ Varies | Any assistant that reads markdown |

### Requirements

- Git (any recent version)
- GitHub, GitLab, or Bitbucket
- AI coding assistant (see above)

---

## What's Included

```
DevRails/
├── README.md                     # You are here
├── LICENSE                       # MIT License
├── CONTRIBUTING.md               # How to contribute
│
├── docs/dev/                     # Standards package
│   ├── README.md                 # Detailed documentation
│   ├── COMMANDS.md               # Full command reference
│   ├── SETUP.md                  # Complete installation guide
│   ├── MEMORIES.md               # AI persistent instructions
│   ├── BREADCRUMB_TEMPLATE.md    # Project integration template
│   │
│   ├── standards/                # Workflow documentation
│   │   ├── pull-request-workflow.md
│   │   ├── defect-workflow.md
│   │   ├── git-workflow.md
│   │   ├── code-review-standards.md
│   │   └── ...
│   │
│   ├── definitions/              # Terminology
│   │   ├── glossary.md           # 60+ terms defined
│   │   └── work-types.md
│   │
│   ├── templates/                # Reusable templates
│   │   ├── org-claude-md.template
│   │   ├── project-claude-md.template
│   │   ├── pull-request-template.md
│   │   └── ...
│   │
│   └── decisions/                # Architecture decisions
│
└── .claude/                      # AI integration
    ├── MEMORIES.md               # AI persistent memory
    ├── commands/                 # Slash commands
    │   ├── fix.md
    │   ├── feature.md
    │   ├── pr.md
    │   ├── commit.md
    │   ├── review.md
    │   └── status.md
    └── skills/                   # Proactive AI behavior
        └── dev-workflow/
            ├── SKILL.md
            └── workflows.md
```

---

## Installation Options

### Option A: Full Installation (Recommended)

Copy everything to your org:

```bash
# Clone
git clone https://github.com/AssistantCompany/DevRails.git

# Copy to your org
cp -r DevRails/docs/dev /your/org/docs/dev
cp -r DevRails/.claude /your/org/.claude
cp DevRails/docs/dev/templates/org-claude-md.template /your/org/CLAUDE.md

# Edit CLAUDE.md with your org details
```

### Option B: Submodule

Add as a git submodule:

```bash
git submodule add https://github.com/AssistantCompany/DevRails.git devrails
```

### Option C: Manual Copy

Download ZIP from GitHub and copy `docs/dev/` and `.claude/` to your org.

---

## Integrating Existing Projects

DevRails is **brownfield-safe** - it merges with existing projects without overwriting.

### If project has NO CLAUDE.md:

```bash
cp docs/dev/templates/project-claude-md.template projects/myproject/CLAUDE.md
# Edit with project-specific details
```

### If project HAS CLAUDE.md:

Add this section at the top (don't replace existing content):

```markdown
## Organization Standards (DevRails)

This project follows DevRails development standards.

Commands: /fix, /feature, /pr, /commit, /review, /status

See: ../../docs/dev/README.md
```

---

## Why DevRails?

### Before DevRails

- 📚 30-40 minutes reading docs before first commit
- 🤷 Everyone does things differently
- 🔄 Reinvent processes for every project
- 😵 AI assistants don't know your conventions
- 📝 Standards exist but nobody reads them

### After DevRails

- ⚡ **Instant** - Just use `/fix` or `/feature`
- 🎯 **Consistent** - Same workflow everywhere
- 🔧 **Automated** - AI handles complexity
- 📦 **Portable** - Works on any server
- 🧠 **AI-First** - Built for AI assistants

---

## Documentation

| Document | Description |
|----------|-------------|
| [docs/dev/COMMANDS.md](docs/dev/COMMANDS.md) | All commands with examples |
| [docs/dev/SETUP.md](docs/dev/SETUP.md) | Complete installation guide |
| [docs/dev/standards/](docs/dev/standards/) | Detailed workflow docs |
| [docs/dev/definitions/glossary.md](docs/dev/definitions/glossary.md) | All terminology |

---

## Key Principles

1. **One branch = one PR = one unit of work**
2. **PR is the container**, not the problem
3. **Simple commands**, complex workflows underneath
4. **AI-first** - designed for AI assistants
5. **Portable** - relative paths, works anywhere
6. **Brownfield-safe** - merges, never overwrites

---

## Contributing

Contributions welcome! See [CONTRIBUTING.md](CONTRIBUTING.md).

---

## License

MIT License - see [LICENSE](LICENSE).

---

<p align="center">
  <br>
  <b>DevRails</b><br>
  Keep your development on track.
  <br><br>
  ⭐ Star this repo if it helps you!
</p>

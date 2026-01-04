<p align="center">
  <img src="https://img.shields.io/badge/DevRails-Keep%20Development%20On%20Track-blue?style=for-the-badge" alt="DevRails">
</p>

<h1 align="center">DevRails</h1>

<p align="center">
  <b>Keep your development on track.</b><br>
  A portable development standards package for <b>Claude Code</b> that automates workflows and keeps teams consistent.
</p>

<p align="center">
  <a href="#quick-start"><img src="https://img.shields.io/badge/Setup-5%20minutes-brightgreen?style=flat-square" alt="Setup Time"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square" alt="License: MIT"></a>
  <a href="#prerequisites"><img src="https://img.shields.io/badge/Requires-Claude%20Code-blueviolet?style=flat-square" alt="Requires Claude Code"></a>
  <a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-Welcome-brightgreen?style=flat-square" alt="PRs Welcome"></a>
</p>

<p align="center">
  <a href="#prerequisites">Prerequisites</a> •
  <a href="#quick-start">Quick Start</a> •
  <a href="#commands">Commands</a> •
  <a href="#how-it-works">How It Works</a>
</p>

---

## Prerequisites

> ⚠️ **DevRails requires [Claude Code](https://claude.ai/code)** - Anthropic's official AI coding assistant.

| Requirement | Status | Notes |
|-------------|--------|-------|
| **Claude Code** | **Required** | Slash commands and proactive skills only work with Claude Code |
| **Git** | Required | Version control |
| **GitHub/GitLab** | Required | For PR integration |

### Why Claude Code Only?

DevRails uses Claude Code's native features:

| Feature | Location | What It Does |
|---------|----------|--------------|
| **Slash Commands** | `.claude/commands/` | `/fix`, `/feature`, `/pr`, `/commit`, `/review`, `/status` |
| **Proactive Skills** | `.claude/skills/` | Auto-triggers on keywords, warns on main branch |
| **AI Memory** | `.claude/MEMORIES.md` | Persistent instructions across sessions |

These are **Claude Code specific** and won't work with other AI assistants.

> 📝 **Note:** The documentation in `docs/dev/` (workflows, glossary, templates) can be read by any AI assistant for reference, but you won't get the automated slash commands without Claude Code.

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

Claude:    Creating bugfix/login-authentication-error branch...
           [fixes issue, adds test, commits properly]
           Ready for PR. Run /pr to create it.
```

**One command. Done.**

---

## Quick Start

### Step 1: Install Claude Code

If you don't have Claude Code installed:

```bash
# See installation instructions at:
# https://claude.ai/code
```

### Step 2: Clone DevRails

```bash
git clone https://github.com/AssistantCompany/DevRails.git
cd DevRails
```

### Step 3: Copy to Your Organization

```bash
# Copy docs/dev/ to your org root
cp -r docs/dev /path/to/your/org/docs/dev

# Copy .claude/ to your org root (REQUIRED for commands)
cp -r .claude /path/to/your/org/.claude
```

### Step 4: Create Org CLAUDE.md

```bash
cp docs/dev/templates/org-claude-md.template /path/to/your/org/CLAUDE.md
# Edit with your org name and project list
```

### Step 5: Start Using

Open Claude Code in your org directory:

```bash
cd /path/to/your/org
claude
```

Then use commands:

```
/status                    # Shows current state
/fix <bug description>     # Fixes a bug
/feature <description>     # Adds a feature
/pr                        # Creates pull request
```

**That's it. You're on track.**

---

## Commands

| Command | What You Say | What Claude Does |
|---------|--------------|------------------|
| `/fix <description>` | "Fix the login bug" | Creates `bugfix/` branch, investigates, fixes, adds test, commits with `fix:` |
| `/feature <description>` | "Add dark mode" | Creates `feature/` branch, implements, tests, commits with `feat:` |
| `/pr` | "Create a PR" | Pushes branch, creates PR with template, links issues |
| `/commit` | "Commit this" | Formats message with conventional commit style |
| `/review` | "Review this code" | Checks security, tests, quality, performance |
| `/status` | "Where am I?" | Shows branch, changes, suggests next action |

### Natural Language Works Too

You don't need slash commands. Just describe what you want:

| You Say | Claude Does |
|---------|-------------|
| "Fix the authentication bug" | Starts bugfix workflow |
| "Add user settings page" | Starts feature workflow |
| "I'm done with this" | Suggests creating PR |

---

## How It Works

### What You Do vs What Claude Does

#### Bug Fix Flow

| Step | Who | Action |
|------|-----|--------|
| 1 | **You** | `/fix null pointer in auth` |
| 2 | **Claude** | Creates `bugfix/null-pointer-in-auth` branch |
| 3 | **Claude** | Searches code, identifies root cause |
| 4 | **Claude** | Implements fix |
| 5 | **Claude** | Adds regression test |
| 6 | **Claude** | Commits: `fix: resolve null pointer in auth` |
| 7 | **Claude** | "Ready for PR?" |
| 8 | **You** | "Yes" or `/pr` |
| 9 | **Claude** | Creates PR with template |

#### Feature Flow

| Step | Who | Action |
|------|-----|--------|
| 1 | **You** | `/feature dark mode` |
| 2 | **Claude** | Creates `feature/dark-mode` branch |
| 3 | **Claude** | Implements feature |
| 4 | **Claude** | Adds tests |
| 5 | **Claude** | Commits: `feat: add dark mode` |
| 6 | **Claude** | "Ready for PR?" |

### Proactive Behavior

Claude will automatically:
- **Warn** if you're on `main` branch
- **Suggest** correct branch prefix
- **Format** commits conventionally
- **Remind** you to add tests
- **Link** PRs to issues

---

## What's Included

```
DevRails/
├── README.md                     # You are here
├── LICENSE                       # MIT License
├── CONTRIBUTING.md               # How to contribute
│
├── .claude/                      # ⚡ CLAUDE CODE SPECIFIC
│   ├── MEMORIES.md               # AI persistent memory
│   ├── commands/                 # Slash commands
│   │   ├── fix.md               # /fix
│   │   ├── feature.md           # /feature
│   │   ├── pr.md                # /pr
│   │   ├── commit.md            # /commit
│   │   ├── review.md            # /review
│   │   └── status.md            # /status
│   └── skills/                   # Proactive AI
│       └── dev-workflow/
│           ├── SKILL.md
│           └── workflows.md
│
└── docs/dev/                     # 📚 Standards documentation
    ├── README.md
    ├── COMMANDS.md
    ├── SETUP.md
    ├── standards/                # Workflow docs
    ├── definitions/              # Glossary
    └── templates/                # PR, commit templates
```

---

## Installation

### Full Installation (Recommended)

```bash
# Clone
git clone https://github.com/AssistantCompany/DevRails.git

# Copy BOTH directories to your org
cp -r DevRails/docs/dev /your/org/docs/dev
cp -r DevRails/.claude /your/org/.claude

# Create org CLAUDE.md
cp DevRails/docs/dev/templates/org-claude-md.template /your/org/CLAUDE.md
```

### Integrating Existing Projects

DevRails is **brownfield-safe** - merges without overwriting.

**If project has CLAUDE.md:** Add this at the top (keep existing content):

```markdown
## Organization Standards (DevRails)

Commands: /fix, /feature, /pr, /commit, /review, /status
See: ../../docs/dev/README.md
```

**If project has NO CLAUDE.md:**

```bash
cp docs/dev/templates/project-claude-md.template projects/myproject/CLAUDE.md
```

---

## Why DevRails?

| Before | After |
|--------|-------|
| 📚 30-40 min reading docs | ⚡ Just use `/fix` |
| 🤷 Everyone does it different | 🎯 Same workflow everywhere |
| 🔄 Reinvent for each project | 📦 Portable standards |
| 📝 Standards nobody reads | 🧠 Claude knows them |

---

## Documentation

| Document | Description |
|----------|-------------|
| [docs/dev/COMMANDS.md](docs/dev/COMMANDS.md) | Full command reference |
| [docs/dev/SETUP.md](docs/dev/SETUP.md) | Complete installation guide |
| [docs/dev/standards/](docs/dev/standards/) | Workflow documentation |
| [docs/dev/definitions/glossary.md](docs/dev/definitions/glossary.md) | 60+ terms defined |

---

## Key Principles

1. **One branch = one PR = one unit of work**
2. **PR is the container**, not the problem
3. **Simple commands**, complex workflows underneath
4. **Claude Code native** - built for Claude's features
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
  Built for <a href="https://claude.ai/code">Claude Code</a>
  <br><br>
  ⭐ Star if it helps!
</p>

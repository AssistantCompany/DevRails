<p align="center">
  <img src="https://img.shields.io/badge/DevRails-Keep%20Development%20On%20Track-blue?style=for-the-badge" alt="DevRails">
</p>

<h1 align="center">DevRails</h1>

<p align="center">
  <b>Keep your development on track.</b><br>
  A portable development standards package for <b>Claude Code</b> that automates workflows and keeps teams consistent.
</p>

<p align="center">
  <a href="#quick-start"><img src="https://img.shields.io/badge/Get%20Started-2%20minutes-brightgreen?style=flat-square" alt="Get Started"></a>
  <a href="LICENSE"><img src="https://img.shields.io/badge/License-MIT-blue?style=flat-square" alt="License: MIT"></a>
  <a href="#requirements"><img src="https://img.shields.io/badge/Requires-Claude%20Code-blueviolet?style=flat-square" alt="Requires Claude Code"></a>
  <a href="CONTRIBUTING.md"><img src="https://img.shields.io/badge/PRs-Welcome-brightgreen?style=flat-square" alt="PRs Welcome"></a>
</p>

<p align="center">
  <a href="#what-is-devrails">What is DevRails?</a> •
  <a href="#quick-start">Quick Start</a> •
  <a href="#features">Features</a> •
  <a href="#commands">Commands</a> •
  <a href="#requirements">Requirements</a>
</p>

---

## Requirements

> **DevRails requires [Claude Code](https://claude.ai/code)** - Anthropic's official AI coding assistant.

| Requirement | Status | Notes |
|-------------|--------|-------|
| **Claude Code** | **Required** | Slash commands and proactive skills are Claude Code specific |
| **Git** | Required | Version control |
| **GitHub/GitLab** | Required | For PR integration |

### Why Claude Code?

DevRails uses Claude Code's native features:

| Feature | Location | What It Does |
|---------|----------|--------------|
| **Slash Commands** | `.claude/commands/` | `/fix`, `/feature`, `/pr`, `/commit`, `/review`, `/status` |
| **Proactive Skills** | `.claude/skills/` | Auto-triggers on keywords, warns on main branch |
| **AI Memory** | `.claude/MEMORIES.md` | Persistent instructions across sessions |

> **Note:** The documentation in `docs/dev/` (workflows, glossary, templates) can be read by any AI assistant for reference, but the automated slash commands require Claude Code.

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

## What is DevRails?

**DevRails** is a drop-in development standards package that works with Claude Code to automate your workflows.

Instead of reading thousands of lines of documentation, you just use simple commands:

```bash
/fix login bug          # Creates branch, guides fix, adds test, opens PR
/feature dark-mode      # Creates branch, implements, commits conventionally
/pr                     # Opens PR with proper template
```

**Claude handles the complexity. You just describe what you want.**

---

## Quick Start

### 1. Install (2 minutes)

```bash
# Clone DevRails
git clone https://github.com/AssistantCompany/DevRails.git

# Copy to your organization
cp -r DevRails/docs/dev /path/to/your/org/docs/dev
cp -r DevRails/.claude /path/to/your/org/.claude
```

### 2. Use (immediately)

Open Claude Code in your org directory and start using commands:

```
/status                 # See where you are
/fix <bug description>  # Fix a bug
/feature <description>  # Add a feature
/pr                     # Create pull request
```

That's it. You're on track.

---

## Commands

| Command | What It Does |
|---------|--------------|
| `/fix <description>` | Start bugfix workflow - creates branch, guides fix, adds test |
| `/feature <description>` | Start feature workflow - creates branch, implements |
| `/pr` | Create pull request with proper template and issue linking |
| `/commit` | Format commit message with conventional commit style |
| `/review` | Review code against security, quality, and test checklist |
| `/status` | Show current state and suggest next action |

### Natural Language Works Too

Just describe what you want:

- *"Fix the authentication bug"* → Triggers bugfix workflow
- *"Add user settings page"* → Triggers feature workflow
- *"I'm done with this feature"* → Suggests creating PR

---

## Features

| Feature | Description |
|---------|-------------|
| **Simple Commands** | 6 slash commands replace reading documentation |
| **Proactive Guidance** | Claude warns if you're on main, suggests correct branch names |
| **Conventional Commits** | Automatic formatting of commit messages |
| **PR Automation** | Creates PRs with templates and issue linking |
| **Code Review Checklist** | Built-in standards for security, tests, quality |
| **Portable** | Drop on any server, works immediately |
| **Brownfield-Safe** | Merges with existing projects, never overwrites |

---

## What's Included

```
docs/dev/
├── README.md                 # You are here
├── COMMANDS.md               # Full command reference
├── SETUP.md                  # Installation guide
├── LICENSE                   # MIT License
├── CONTRIBUTING.md           # How to contribute
│
├── standards/                # Workflow documentation
│   ├── pull-request-workflow.md
│   ├── defect-workflow.md
│   ├── git-workflow.md
│   ├── code-review-standards.md
│   └── ...
│
├── definitions/              # Terminology
│   ├── glossary.md           # 60+ terms defined
│   └── work-types.md         # Feature vs Bug vs Task
│
├── templates/                # Reusable formats
│   ├── pull-request-template.md
│   ├── commit-message-template.md
│   └── ...
│
└── decisions/                # Architecture decisions (ADRs)

.claude/
├── commands/                 # Slash commands (/fix, /feature, etc.)
├── skills/                   # Proactive AI behavior
└── MEMORIES.md               # AI persistent memory
```

---

## Why DevRails?

### Before DevRails

- 30-40 minutes reading documentation before your first commit
- Everyone does things differently
- Reinvent processes for every new project
- AI assistants don't know your conventions
- Standards exist but nobody reads them

### After DevRails

- **Instant** - Just use `/fix` or `/feature`
- **Consistent** - Everyone follows the same workflow
- **Automated** - Claude handles the complexity
- **Portable** - Works on any server
- **Claude Code Native** - Built specifically for Claude Code

---

## Installation

See [SETUP.md](./SETUP.md) for complete installation instructions.

**Quick version:**

1. Copy `docs/dev/` to your org root
2. Copy `.claude/` to your org root
3. Create org-level `CLAUDE.md` pointing to standards
4. Add breadcrumb to each project's `CLAUDE.md`

DevRails handles both **greenfield** (new) and **brownfield** (existing) projects without overwriting your existing configuration.

---

## Documentation

| Document | Description |
|----------|-------------|
| [COMMANDS.md](./COMMANDS.md) | All commands with examples |
| [SETUP.md](./SETUP.md) | Installation and configuration |
| [CONTRIBUTING.md](./CONTRIBUTING.md) | How to contribute |
| [standards/](./standards/) | Detailed workflow documentation |
| [definitions/glossary.md](./definitions/glossary.md) | All terminology defined |
| [templates/](./templates/) | PR, commit, and issue templates |

---

## Key Principles

1. **One branch = one PR = one unit of work**
2. **PR is the container**, not the problem
3. **Simple commands**, complex workflows underneath
4. **Claude Code native** - built for Claude's features
5. **Portable** - works on any server with relative paths
6. **Brownfield-safe** - merges, never overwrites

---

## Contributing

Contributions are welcome! Please see [CONTRIBUTING.md](./CONTRIBUTING.md) for guidelines.

---

## License

MIT License - see [LICENSE](./LICENSE) for details.

---

<p align="center">
  <br>
  <b>DevRails</b><br>
  Keep your development on track.
  <br><br>
  Built for <a href="https://claude.ai/code">Claude Code</a>
  <br><br>
  <a href="#quick-start">Get Started →</a>
</p>

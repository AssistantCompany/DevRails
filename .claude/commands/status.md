---
description: Show current development state and suggest next actions based on context
allowed-tools: Bash, Read, Grep
---

# Development Status

You are checking the current development state and suggesting next actions.

## Steps

1. **Check git state**
   ```bash
   git status
   git branch --show-current
   git log --oneline -5
   ```

2. **Analyze current situation**

   ### If on `main` branch:
   - Warn: "You're on main. Create a branch before making changes."
   - Suggest: `/fix <description>` or `/feature <description>`

   ### If on feature/bugfix branch:
   - Show branch name and type
   - Show commits ahead of main
   - Show uncommitted changes

   ### If uncommitted changes exist:
   - List modified files
   - Suggest: `/commit` to commit changes
   - Or ask if changes should be stashed

   ### If commits ready but not pushed:
   - Show commits not on remote
   - Suggest: Push and create PR with `/pr`

   ### If branch is pushed:
   - Check if PR exists: `gh pr view --json state,url 2>/dev/null`
   - If PR exists, show its status
   - If no PR, suggest creating one

3. **Check for open issues (optional)**
   - Run `gh issue list --limit 5` if available
   - Mention any assigned issues

4. **Provide recommendations**
   Based on state, suggest the logical next action:
   - On main with no changes → "What would you like to work on?"
   - On branch with changes → `/commit`
   - On branch, committed → `/pr`
   - PR open → "Waiting for review" or address feedback

5. **Quick summary format**
   ```
   Branch: feature/add-dark-mode
   Status: 3 commits ahead of main, 2 files modified
   Next: Commit your changes with /commit, then /pr
   ```

## Reference
Git workflow: docs/dev/standards/git-workflow.md
PR workflow: docs/dev/standards/pull-request-workflow.md

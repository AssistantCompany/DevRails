# Quick Workflow Reference

## Bugfix Workflow (defect)
```
1. Create branch: bugfix/<description>
2. Investigate → Find root cause
3. Fix → Minimal, focused change
4. Test → Add regression test
5. Commit → fix: <description>
6. PR → Link to issue with "Fixes #123"
```

## Feature Workflow
```
1. Create branch: feature/<description>
2. Implement → Follow existing patterns
3. Test → Unit + integration tests
4. Commit → feat: <description>
5. PR → Describe what and why
```

## Commit Types
| Type | Use For |
|------|---------|
| `feat:` | New feature |
| `fix:` | Bug fix |
| `docs:` | Documentation |
| `style:` | Formatting |
| `refactor:` | Restructure |
| `test:` | Tests |
| `chore:` | Maintenance |

## Branch Prefixes
| Prefix | Use For |
|--------|---------|
| `feature/` | New capability |
| `bugfix/` | Bug fix |
| `task/` | Technical work |
| `chore/` | Maintenance |

## PR Checklist
- [ ] Branch is not `main`
- [ ] All changes committed
- [ ] Tests pass
- [ ] Clear description
- [ ] Issue linked (if applicable)

## Code Review Checklist
- [ ] Correctness
- [ ] Tests
- [ ] Security
- [ ] Performance
- [ ] Code quality
- [ ] Documentation

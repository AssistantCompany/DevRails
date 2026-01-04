# Architectural Decision Records (ADRs)

> Documenting important decisions and their context.

## What is an ADR?

An **Architectural Decision Record (ADR)** captures:
- A significant decision
- The context and constraints
- The decision made
- The consequences

ADRs are "decision logs" that help future developers understand **why** things are the way they are.

---

## When to Write an ADR

Write an ADR when:
- Choosing a technology or library
- Defining a significant pattern
- Making a breaking change
- Establishing a new process
- Deviating from existing conventions

---

## ADR Index

| ID | Title | Status | Date |
|----|-------|--------|------|
| [0001](./0001-documentation-structure.md) | Documentation Structure | Accepted | 2026-01-04 |

---

## Status Types

| Status | Meaning |
|--------|---------|
| **Proposed** | Under discussion, not yet decided |
| **Accepted** | Decision made and in effect |
| **Deprecated** | No longer applies, but preserved for history |
| **Superseded** | Replaced by another ADR (link to new one) |

---

## How to Write an ADR

1. Copy the [ADR template](./adr-template.md)
2. Create new file: `NNNN-short-title.md`
3. Fill in all sections
4. Submit PR for review
5. Update this index when accepted

### Naming Convention

```
0001-short-descriptive-title.md
0002-another-decision.md
```

- Use sequential numbers (0001, 0002, ...)
- Use lowercase with hyphens
- Keep title short but descriptive

---

## Template

See [adr-template.md](./adr-template.md) for the full template.

Quick structure:
```markdown
# ADR-NNNN: Title

## Status
Accepted | Proposed | Deprecated | Superseded

## Context
What is the issue or need?

## Decision
What did we decide?

## Consequences
What are the results?
```

---

## Best Practices

### Do
- Keep ADRs brief and focused
- Write as decisions are made
- Include context for future readers
- Update status when things change
- Link related ADRs

### Don't
- Rewrite history (preserve original)
- Include implementation details
- Wait too long to document
- Make ADRs too long

---
name: handoff
description: Create context transfer documents for thread transitions. Use when work spans multiple sessions or when context window is filling up.
---

# Handoff

Create structured context transfers between threads or sessions.

## When to Use
- Thread context approaching limits
- Work will continue in new thread
- Switching focus to different task
- End of work session
- Before using Amp's built-in handoff feature

## Handoff Document Format

Create in `amp-os/handoffs/[feature]-[date].md`:

```markdown
# Handoff: [Feature Name]

## Status
- **Phase**: [planning|implementing|testing|verifying]
- **Progress**: [X of Y tasks complete]
- **Blockers**: [any blocking issues]

## Completed Work
- [List of completed items with file paths]

## In Progress
- [Current task being worked on]
- [Any partial work to note]

## Next Steps
1. [Immediate next action]
2. [Following action]
3. [...]

## Key Decisions Made
- [Decision]: [Rationale]

## Files Modified
- `path/to/file.ts` - [what changed]

## Context for Next Thread
[Any important context the next thread needs to know]
```

## Creating a Handoff

1. **Summarize current state** - What's done, what's not
2. **List concrete next steps** - Actionable items
3. **Note key decisions** - So they're not revisited
4. **Reference file paths** - Specific locations, not vague

## Using a Handoff

When starting new thread:
1. Read the handoff document
2. Verify file states match handoff
3. Continue from "Next Steps"

## Amp Integration

Use Amp's built-in handoff feature:
- Amp extracts relevant context automatically
- Creates new thread with handoff prompt
- Use `@@` to reference original thread if needed

### Thread Mention Syntax
```
@@thread-name - pulls context from that thread
```

## Quick Handoff Template

For simple transitions:

```markdown
# Quick Handoff: [Feature]

**Done:** [bullet list]
**Next:** [immediate action]
**Files:** [key files touched]
**Note:** [one critical context item]
```

## Anti-Patterns

- Vague summaries ("worked on auth")
- Missing file paths
- No next steps
- Repeating entire conversation history
- Forgetting key decisions made

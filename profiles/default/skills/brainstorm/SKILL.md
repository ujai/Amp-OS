---
name: brainstorm
description: Socratic pre-planning before any implementation. Use before plan-product to refine ideas into validated designs through structured dialogue.
---

# Brainstorm

Transform vague ideas into validated designs before writing any code.

## When to Use
- Before `plan-product` for new features
- When requirements are unclear
- When multiple approaches seem viable
- Before any significant implementation work

## Workflow

### Phase 1: Understand the Idea

1. **Check project context first**
   - Read existing specs, roadmap, AGENTS.md
   - Understand current architecture

2. **Ask clarifying questions**
   - One question per message (don't overwhelm)
   - Prefer multiple-choice when possible
   - Focus on: purpose, constraints, success criteria

### Phase 2: Explore Approaches

1. **Present 2-3 options** with trade-offs
2. **Lead with your recommendation** and explain why
3. **Frame choices conversationally**

### Phase 3: Present the Design

1. **Break into 200-300 word sections**
   - Architecture overview
   - Key components
   - Data flow
   - Error handling
   - Testing approach

2. **Validate after each section**
   - "Does this look right so far?"
   - Be ready to backtrack and clarify

## Key Principles

- **One question at a time** - Don't overwhelm
- **YAGNI ruthlessly** - Remove unnecessary features
- **Explore alternatives** - Never settle on first idea
- **Incremental validation** - Section by section approval

## Output

Write validated design to:
```
amp-os/specs/[feature]/design.md
```

Then proceed to `amp-os-plan-product` to create roadmap.

## Example Questions

**Understanding purpose:**
- "What problem does this solve for the user?"
- "What's the minimum viable version of this feature?"

**Multiple choice (preferred):**
```
For authentication, which approach fits best?
A) JWT tokens (stateless, good for APIs)
B) Session cookies (simpler, good for web apps)
C) OAuth only (delegate to providers)
```

**Constraints:**
- "Are there performance requirements?"
- "Does this need to work offline?"

## Anti-Patterns

- Jumping straight to implementation
- Asking multiple questions at once
- Accepting vague requirements
- Skipping the exploration phase
- Designing without understanding context

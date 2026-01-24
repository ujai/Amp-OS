---
name: implement-tasks
description: Implement tasks from tasks.md using TDD and optional multi-agent orchestration. Includes two-stage review and handoff support.
---

# Implement Tasks

Execute implementation using structured task groups with verification loops.

## When to Use
- tasks.md is complete and approved
- Ready to write code
- Need TDD-first implementation workflow

## Workflow

### 1. Load Context
- Read `amp-os/specs/[feature]/tasks.md`
- Read `amp-os/specs/[feature]/spec.md`
- Load relevant standards: `amp-os-standards-global`, backend/frontend as needed

### 2. For Each Task Group (in dependency order)

#### a. Write Tests First (RED)
- Write all tests defined for the group
- Tests should initially fail
- Cover happy path, edge cases, error scenarios

#### b. Implement (GREEN)
- Write minimum code to pass tests
- Follow loaded standards strictly
- Keep functions small and focused

#### c. Refactor
- Clean up while keeping tests green
- Extract common patterns
- Improve naming and structure

#### d. Verify Group
- All group tests pass
- Code follows standards
- No type errors or lint warnings

#### e. Self-Review (Two Stages)

**Stage 1: Spec Compliance**
- Does implementation match spec requirements?
- Are all acceptance criteria met?
- Any deviations to note?

**Stage 2: Code Quality**
- Follows project patterns?
- Error handling complete?
- No security issues?

#### f. Update Progress
- Mark tasks complete in tasks.md
- Create handoff if switching threads

### 3. Track Progress
- Update tasks.md checkboxes directly
- Create handoff document for long implementations

## Implementation Modes

### Single-Agent Mode (Default)
Process task groups sequentially yourself.

### Subagent Mode (Complex Features)
Use `Task` tool to delegate task groups:

```
Task: "Implement Task Group 1 (Database Layer)"

Context:
- Spec: amp-os/specs/[feature]/spec.md
- Tasks: amp-os/specs/[feature]/tasks.md (Group 1 only)

Instructions:
- Load amp-os-standards-backend skill
- Follow TDD: write tests first
- Run only group-specific tests
- Create handoff when complete with:
  - Files modified
  - Tests added
  - Any issues encountered
```

## Resources
- [Implementation Workflow](resources/implementation-workflow.md)

## Amp Tools to Use
- `Task` - Delegate to sub-agents (can write to codebase)
- `finder` - Find related code
- `Librarian` - Search documentation for patterns
- Standard file editing tools

## Important Rules

1. **Tests first** - Always write tests before implementation
2. **Group isolation** - Only run tests for current group
3. **No skipping** - Complete groups in dependency order
4. **Two-stage review** - Verify spec compliance AND code quality
5. **Handoffs for breaks** - Create handoff if pausing work
6. **Short threads** - Use new thread per task group if complex

## Anti-Patterns

- Implementing without tests
- Skipping the self-review stages
- Long threads spanning multiple task groups
- Vague task updates ("worked on auth")

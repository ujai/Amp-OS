---
name: workflow-orchestrator
description: Chain multiple skills for complete feature development. Coordinates plan to implement to verify with handoffs between phases.
---

# Workflow Orchestrator

Chain skills together for end-to-end feature development.

## Workflows

### Greenfield (New Feature)
```
brainstorm → plan-product → shape-spec → write-spec → create-tasks → implement-tasks → verify-implementation
```

### Brownfield (Existing Codebase)
```
[analyze existing] → shape-spec → write-spec → create-tasks → implement-tasks → verify-implementation
```

### Bug Fix
```
[investigate] → create-tasks → implement-tasks → verify-implementation
```

### Refactor
```
[impact analysis] → create-tasks → implement-tasks → verify-implementation
```

## Usage

```
"Load amp-os-workflow-orchestrator"
"Start greenfield workflow for [feature description]"
```

## Execution Modes

### Sequential (Default)
Process each phase yourself, creating handoffs between major phases.

### Subagent Mode
Delegate phases to subagents:

```
Task: "Execute shape-spec phase for [feature]"

Context:
- Feature: [name]
- Design doc: amp-os/specs/[feature]/design.md
- Output to: amp-os/specs/[feature]/requirements.md

Instructions:
- Load amp-os-shape-spec skill
- Research requirements thoroughly
- Create handoff when complete
```

## Phase Boundaries

Create handoffs at these checkpoints:
1. After `brainstorm` → before `plan-product`
2. After `write-spec` → before `create-tasks`
3. After each task group in `implement-tasks`
4. After `implement-tasks` → before `verify-implementation`

## Human Checkpoints

Pause for approval at:
- Design validation (after brainstorm)
- Spec approval (after write-spec)
- Implementation review (after implement-tasks)
- Final verification (after verify-implementation)

## Thread Patterns

### Hub-and-Spokes
Best for: Feature development with multiple implementation tracks

```
         [Planning Hub]
              │
    ┌─────────┼─────────┐
    │         │         │
    ▼         ▼         ▼
[Backend]  [Frontend]  [Tests]
  Spoke      Spoke      Spoke
```

- **Hub**: Contains brainstorm, plan, spec (reference thread)
- **Spokes**: Implementation threads (one per task group)
- Use `@@planning-thread` to reference decisions

### Chain Pattern
Best for: Sequential workflows where each phase builds on previous

```
[Brainstorm] → handoff → [Plan] → handoff → [Implement] → handoff → [Verify]
```

- Short, focused threads
- Handoff documents bridge context
- Clean context at each phase

## Workflow State Tracking

Create `amp-os/specs/[feature]/workflow-state.md`:

```markdown
# Workflow: [Feature]

## Current Phase
[phase name]

## Completed Phases
- [x] brainstorm - design.md created
- [x] plan-product - roadmap updated
- [ ] shape-spec
- [ ] write-spec
- [ ] create-tasks
- [ ] implement-tasks
- [ ] verify-implementation

## Handoffs
- brainstorm → plan: `handoffs/feature-2026-01-25-design.md`

## Thread References
- Planning: @@feature-planning
- Backend: @@feature-backend
```

## Amp Tools to Use
- `Task` - Delegate phases to subagents
- `skill` - Load phase-specific skills
- `finder` - Search codebase
- `oracle` - Review and planning assistance

## Best Practices

1. **Keep threads short** - One phase or task group per thread
2. **Use handoffs** - Don't let context fill up
3. **Reference, don't repeat** - Use `@@` for cross-thread context
4. **Subagents for parallel work** - Explicitly delegate independent tasks
5. **Plan first, execute second** - Iterate plan until solid, then implement
6. **Human checkpoints** - Get approval at phase boundaries

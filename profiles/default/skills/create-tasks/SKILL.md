---
name: create-tasks
description: Break a specification into implementable tasks with exact file paths and clear acceptance criteria.
---

# Create Tasks

Transform specification into actionable task groups.

## When to Use
- Specification (spec.md) is complete and approved
- Ready to plan implementation
- Need clear, granular tasks

## Workflow

### 1. Load Context
- Read `amp-os/specs/[feature]/spec.md`
- Read `amp-os/specs/[feature]/requirements.md`
- Scan existing codebase for patterns (`finder`)

### 2. Identify Task Groups

Group by dependency order:
1. **Foundation** - Core types, schemas, config
2. **Data Layer** - Database, models, migrations
3. **Business Logic** - Services, core functions
4. **API Layer** - Endpoints, handlers
5. **UI Layer** - Components, pages (if applicable)
6. **Integration** - Wiring, final connections

### 3. Create Tasks

For each task, include:

```markdown
### Task 1.1: [Descriptive Name]

**Files:**
- `src/types/[feature].ts` - Create types
- `src/services/[feature].service.ts` - Implement service

**Tests:**
- `src/__tests__/[feature].service.test.ts`

**Acceptance Criteria:**
- [ ] Types exported and documented
- [ ] Service handles [specific case]
- [ ] Tests cover happy path + error cases

**Dependencies:** None (or list task IDs)
```

### 4. Task Granularity

**Good task size:**
- Completes in one focused session
- Clear start and end state
- Testable independently
- 1-3 files modified

**Split if:**
- Task touches 5+ files
- Multiple independent pieces
- Different expertise needed (backend vs frontend)

### 5. Output Format

Create `amp-os/specs/[feature]/tasks.md`:

```markdown
# Tasks: [Feature Name]

## Overview
- **Total Groups**: N
- **Total Tasks**: M
- **Dependencies**: [diagram or list]

## Group 1: Foundation

### Task 1.1: Create type definitions
**Files:**
- `src/types/feature.ts` - New file

**Tests:**
- Type compilation (no runtime tests needed)

**Acceptance Criteria:**
- [ ] All types from spec defined
- [ ] Exported from index

---

### Task 1.2: ...

## Group 2: Data Layer
...
```

## Resources
- [Task Template](resources/tasks-template.md)
- [Workflow Guide](resources/create-tasks-workflow.md)

## Amp Tools to Use
- `finder` - Find related code patterns
- `Librarian` - Search for similar implementations
- Standard file editing tools

## Important Rules

1. **Exact file paths** - No vague "update the service"
2. **Tests specified** - Every task has test requirements
3. **Clear acceptance criteria** - Checkboxes, not prose
4. **Dependency order** - Groups can be parallelized, tasks within sequential
5. **No time estimates** - Focus on what, not how long

## Anti-Patterns

- Vague tasks ("implement authentication")
- No file paths specified
- Missing test requirements
- Tasks too large (5+ files)
- Circular dependencies

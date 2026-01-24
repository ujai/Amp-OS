---
name: verify-implementation
description: Final verification of completed implementation. Mandatory checklist with AI self-verification before human review.
---

# Verify Implementation

Comprehensive verification after all tasks complete.

## When to Use
- All tasks in tasks.md marked complete
- Ready for final review
- Before merging or deploying

## Verification Process

### Phase 1: AI Self-Verification

Run through this checklist yourself BEFORE presenting to human:

#### Code Quality
- [ ] All tests pass (run the actual test command)
- [ ] No TypeScript/lint errors
- [ ] No `console.log` statements (use proper logging)
- [ ] No commented-out code
- [ ] No TODO comments without ticket references

#### Spec Compliance
- [ ] Every requirement in spec.md is implemented
- [ ] Every acceptance criterion is met
- [ ] No undocumented deviations from spec

#### Standards Compliance
- [ ] Follows patterns in standards-global
- [ ] Backend follows standards-backend (if applicable)
- [ ] Frontend follows standards-frontend (if applicable)
- [ ] Tests follow standards-testing

#### Security
- [ ] No hardcoded secrets
- [ ] Input validation on all external inputs
- [ ] Proper error handling (no stack traces to users)
- [ ] Authentication/authorization correct (if applicable)

#### Documentation
- [ ] README updated if needed
- [ ] API documentation current
- [ ] Complex logic has comments

### Phase 2: Structured Report

Create verification report in `amp-os/specs/[feature]/verification.md`:

```markdown
# Verification Report: [Feature]

## Summary
- **Status**: [PASS | FAIL | PARTIAL]
- **Date**: [YYYY-MM-DD]
- **Verified by**: AI + Human

## Checklist Results

### Code Quality: [PASS/FAIL]
- Tests: [X passed, Y failed]
- Lint: [clean | N issues]
- Notes: [any observations]

### Spec Compliance: [PASS/FAIL]
| Requirement | Status | Notes |
|-------------|--------|-------|
| [req 1] | PASS | |
| [req 2] | PASS | |

### Standards Compliance: [PASS/FAIL]
- [observations]

### Security: [PASS/FAIL]
- [observations]

## Issues Found
1. [Issue description + severity + recommendation]

## Recommendation
[APPROVE | APPROVE WITH NOTES | REQUIRES CHANGES]
```

### Phase 3: Human Review

Present report to human with:
1. Summary status
2. Any issues found
3. Files to review (prioritized by risk)
4. Your recommendation

## Resources
- [Verification Checklist](resources/implementation-verification-checklist.md)
- [Final Report Template](resources/final-report-template.md)

## Amp Tools to Use
- `oracle` - Final review and validation
- Build/test commands from AGENTS.md

## Important Rules

1. **Self-verify first** - Don't just present checklist to human
2. **Run actual tests** - Don't assume they pass
3. **Check every spec item** - No skipping
4. **Be honest about issues** - Flag concerns, don't hide them
5. **Structured output** - Use the report format

## Anti-Patterns

- Skipping AI self-verification
- "Looks good" without running tests
- Missing spec requirements
- Hiding issues to get approval

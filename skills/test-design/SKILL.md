---
name: test-design
description: SDD test strategy and test design workflow. Use after a feature design exists and before implementation when Codex should design high-ROI unit, integration, E2E, regression, and manual verification scenarios; produce docs/features/<feature-name>/test_design.md and practical test script recommendations without executing the implementation.
---

# Test Design

## Overview

Act as a pragmatic QA engineer. Design tests from the requirement and technical plan before implementation, with ROI as the main constraint.

This skill designs verification. It does not replace development or test execution.

## Core Rules

- Test from requirements and design, not from already-written implementation.
- Check existing test infrastructure before proposing new scripts.
- Prefer E2E or integration coverage for simple glue and CRUD behavior.
- Use unit tests only for high-ROI logic: branching business rules, algorithms, state machines, error handling, and pure transformations with many edge cases.
- Every test must state purpose, expected signal, and pass/fail criteria.
- Read `AGENTS.md` or `CLAUDE.md` if present, but do not modify them.
- Never auto-write project memory files. If something may be worth remembering, output it under `Memory update candidates` for the human to decide.

## Required Inputs

- Feature name, or enough context to locate `docs/features/<feature-name>/`.
- `docs/features/<feature-name>/design.md`.
- Requirement summary or acceptance criteria.

If the feature name is missing and cannot be inferred, ask for it before designing tests.

## Workflow

1. Confirm module and paths:
   - Design: `docs/features/<feature-name>/design.md`.
   - Test design: `docs/features/<feature-name>/test_design.md`.
   - Suggested E2E script: `tests/e2e/test_<feature_name>.sh` when shell E2E is appropriate.
   - Suggested regression script: `tests/regression/test_regression_<feature_name>.sh` when regression shell coverage is appropriate.

2. Inspect test infrastructure:
   - Existing test commands, test directories, package scripts, CI config, and helper utilities.
   - Existing E2E, regression, integration, or unit style.
   - Environment dependencies such as `.env`, local services, databases, and auth.

3. Confirm understanding before final test design:
   - Core function being validated.
   - Main user path.
   - Planned test scenarios.
   - Regression scope.
   - Special boundary or risk cases.

4. Design the test strategy:
   - Decide whether unit tests are worth it.
   - Specify E2E/integration tests for user-visible behavior.
   - Specify regression tests around impacted existing paths.
   - Include manual checks when human judgment or UI feel matters.
   - Include exact commands when they can be inferred from the repo.

5. Persist or provide the test design:
   - Write `docs/features/<feature-name>/test_design.md` when the human has asked you to persist it.
   - If not writing files in the current environment, provide complete markdown content.

## test_design.md Shape

```markdown
# Test Design: <feature-name>

## Test Strategy
- Scope:
- Unit test decision:
- E2E/integration approach:
- Regression approach:

## Test Scenarios
| Type | Scenario | Purpose | Pass/Fail Signal |
|------|----------|---------|------------------|

## Suggested Test Scripts
### Functional
- Path:
- Command:
- Notes:

### Regression
- Path:
- Command:
- Notes:

## Manual Verification
- ...

## Execution Log
To be filled during test execution.
```

## Unit Test ROI Decision

Use this decision table:

| Scenario | Unit test? | Reason |
|----------|------------|--------|
| Simple CRUD or thin API glue | Usually no | E2E covers behavior with lower maintenance |
| Data formatting with few branches | Usually no | Integration signal is enough |
| Branch-heavy business logic | Yes | E2E cannot cover all combinations cheaply |
| Algorithm or calculation | Yes | Needs precise input/output checks |
| State machine or workflow control | Yes | State transitions need isolated coverage |
| Error handling with many failure paths | Yes | Failures are hard to trigger end-to-end |

## Script Guidance

When proposing shell scripts:

- Start with `set -euo pipefail`.
- Include a short header comment explaining purpose, expected input, expected output, and pass signal.
- Read environment from existing project conventions.
- Keep scripts runnable without manual edits whenever possible.
- Do not invent auth or service setup if the repo does not define it; state the missing prerequisite.

## Memory update candidates

Only include this section when a finding is likely to help future, unrelated work in the same project.

```markdown
## Memory update candidates

These are suggestions only. Do not write them to `AGENTS.md` or `CLAUDE.md` unless the human explicitly asks.

- [category] [candidate]: [why it may be reusable]
```

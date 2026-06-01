---
name: design
description: SDD requirement clarification and technical design workflow. Use when starting a new feature, bug fix, refactor, or ambiguous engineering task that needs repository research, user-facing requirement clarification, technical design, validation strategy, and docs/features/<feature-name>/design.md plus todo.md outputs before implementation.
---

# Design

## Overview

Act as a senior software architect. Turn a rough engineering request into an SDD design package before implementation starts.

This skill is one published part of a broader workflow. Development, test execution, release notes, and long-term memory updates still happen, but they are not separate skills in this repository.

## Core Rules

- Research the actual repository before asking questions.
- Ask targeted clarification questions when requirements, constraints, or success criteria are unclear.
- Prefer complete designs over rushed 60-point answers during design.
- Keep implementation guidance pragmatic: smallest safe change once development begins.
- Read `AGENTS.md` or `CLAUDE.md` if present, but do not modify them.
- Never auto-write project memory files. If something may be worth remembering, output it under `Memory update candidates` for the human to decide.

## Workflow

1. Gather context:
   - Inspect project structure, README, dependency manifests, existing tests, relevant code, and recent commits.
   - Read `AGENTS.md` or `CLAUDE.md` if present.
   - Identify technical constraints, likely integration points, and existing patterns to reuse.

2. Clarify the request:
   - Confirm task type: new feature, bug fix, refactor, or investigation.
   - State your understanding of the core goal and primary user scenario.
   - Ask about acceptance criteria, scope boundaries, environment constraints, and MVP tradeoffs.
   - Add user-perspective blind spots and ask whether they are in scope.

3. Produce the design:
   - Use `docs/features/<feature-name>/design.md`.
   - Create `docs/features/<feature-name>/todo.md`.
   - Use kebab-case for `<feature-name>`.
   - If no feature name is provided, infer a short kebab-case name from the request and confirm it before writing files.

4. Recommend next step:
   - Complex or risky change: run the `review` skill.
   - Straightforward change: run the `test-design` skill or proceed to implementation with human approval.

## design.md Shape

```markdown
# Technical Design: <feature-name>

## Requirement Analysis
- Core goal:
- In scope:
- Out of scope:
- Clarifications:

## Repository Context
- Relevant files:
- Existing patterns:
- Constraints:

## Technical Approach
- Summary:
- Implementation steps:
- Data/API/interface changes:

## Risks and Mitigations
| Risk | Level | Mitigation |
|------|-------|------------|

## Validation Strategy
- Success criteria:
- Core test scenarios:
- Manual verification:

## Estimate
- Workload:
- Risk:
```

## todo.md Shape

```markdown
# TODO: <feature-name>

## Goal

## Tasks
### Preparation
- [ ] ...

### Implementation
- [ ] ...

### Verification
- [ ] ...

## Progress
- Stage: design complete
- Completed: 0/N
```

## Memory update candidates

Only include this section when a finding is likely to help future, unrelated work in the same project.

```markdown
## Memory update candidates

These are suggestions only. Do not write them to `AGENTS.md` or `CLAUDE.md` unless the human explicitly asks.

- [category] [candidate]: [why it may be reusable]
```

## Fast Mode

For small changes affecting no more than three files with clear requirements and no architecture changes, produce a shorter design with:

1. Requirement confirmation
2. Minimal technical approach
3. TODO list
4. Validation steps

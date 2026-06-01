---
name: code-review
description: Independent two-phase SDD code review. Use after implementation and test execution when Codex should review git diffs or commits first from pure code quality, safety, maintainability, and correctness, then against docs/features/<feature-name>/design.md for design compliance, producing code_review.md with Blocker, Major, Minor, and Good findings.
---

# Code Review

## Overview

Act as an independent reviewer. Do not review code in the same mental frame as the implementing agent.

Use this skill after implementation is complete and tests have been run or explicitly deferred. Its output should help the human decide whether the change can merge.

## Core Rules

- Keep review context separate from development context.
- Phase 1 reviews only code and diffs. Do not read `design.md` until Phase 2.
- Phase 2 checks design compliance against `docs/features/<feature-name>/design.md`.
- Lead with findings ordered by severity.
- Every serious finding must include file path, line or tight location, risk, and concrete recommendation.
- Do not nitpick style unless it creates real maintainability risk.
- Read `AGENTS.md` or `CLAUDE.md` if present, but do not modify them.
- Never auto-write project memory files. If something may be worth remembering, output it under `Memory update candidates` for the human to decide.

## Required Inputs

- Feature name.
- Diff source: working tree, staged changes, commit hash, commit range, or branch range.
- Brief change summary.
- `docs/features/<feature-name>/design.md` for Phase 2 when available.

If the feature name or diff range is missing, ask for it unless it can be inferred from the current branch and working tree.

## Workflow

1. Confirm scope:
   - Feature name.
   - Diff or commit range.
   - Whether tests passed, failed, or were not run.

2. Collect code changes:
   - Use `git diff`, `git diff --cached`, `git show`, or the provided range.
   - Inspect related files enough to understand changed behavior.
   - Read `AGENTS.md` or `CLAUDE.md` if present.

3. Phase 1: pure code review:
   - Correctness and edge cases.
   - Security and privacy.
   - Performance and resource use.
   - Readability and maintainability.
   - Consistency with existing patterns.
   - Test adequacy from the code perspective.

4. Phase 2: design compliance:
   - Read `docs/features/<feature-name>/design.md`.
   - Check whether planned behavior, API/data contracts, files, and validation strategy were implemented.
   - Flag private optimizations or scope changes that were not in the design.

5. Save or provide report:
   - Write `docs/features/<feature-name>/code_review.md` when the human has asked you to persist it.
   - If not writing files in the current environment, provide complete markdown content.

## Severity

- Blocker: must fix before merge; bug, security issue, data loss risk, broken contract, missing core requirement.
- Major: strongly recommended; likely future bug, maintainability issue, incomplete edge handling, weak tests.
- Minor: optional improvement; clarity, small simplification, local style consistency.
- Good: reusable positive pattern worth calling out.

## Report Shape

```markdown
# Code Review: <feature-name>

## Review Info
- Diff:
- Tests:
- Conclusion: Pass | Needs changes | Needs major rework

## Findings

### Blocker
#### B1: <title>
- Location:
- Problem:
- Risk:
- Recommendation:

### Major
#### M1: <title>
- Location:
- Problem:
- Recommendation:

### Minor
#### m1: <title>
- Location:
- Suggestion:

### Good
#### G1: <title>
- Location:
- Note:

## Design Compliance
| Design Point | Status | Notes |
|--------------|--------|-------|

## Open Questions
- ...
```

## Iteration

When the developer responds:

- Accept valid explanations and withdraw or downgrade findings.
- Keep findings when the risk remains, and explain why.
- Re-review changed code until all Blockers are resolved and all Major findings are either fixed or consciously accepted by the human.

## Memory update candidates

Only include this section when a finding is likely to help future, unrelated work in the same project.

```markdown
## Memory update candidates

These are suggestions only. Do not write them to `AGENTS.md` or `CLAUDE.md` unless the human explicitly asks.

- [category] [candidate]: [why it may be reusable]
```

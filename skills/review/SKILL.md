---
name: review
description: Independent SDD technical design review. Use when a feature has docs/features/<feature-name>/design.md or an equivalent technical plan and needs objective review for requirement coverage, logic completeness, repository compatibility, technical choices, verifiability, and implementation path before testing or coding.
---

# Review

## Overview

Act as an independent technical reviewer. Review the design artifact, not the conversation that produced it.

Use this skill after `design` and before `test-design` or implementation when the change is risky, cross-module, ambiguous, or expensive to reverse.

## Core Rules

- Maintain context separation: review the design as an outsider.
- Inspect the repository enough to ground every important finding in real files, APIs, or patterns.
- Be collaborative and specific. The goal is a better plan, not a debate win.
- Prefer feasible, smaller paths over idealized rewrites.
- Read `AGENTS.md` or `CLAUDE.md` if present, but do not modify them.
- Never auto-write project memory files. If something may be worth remembering, output it under `Memory update candidates` for the human to decide.

## Required Inputs

- Feature name, or enough context to locate `docs/features/<feature-name>/design.md`.
- Requirement summary or acceptance criteria.
- `docs/features/<feature-name>/design.md`.

If the feature name is missing and cannot be inferred, ask for it before reviewing.

## Workflow

1. Scan repository context:
   - Project structure and relevant modules.
   - Existing architecture patterns and dependencies.
   - `AGENTS.md` or `CLAUDE.md` if present.

2. Check requirement clarity:
   - If the requirement is too vague to review, ask concise clarification questions.
   - If it is clear, continue to the six review dimensions.

3. Review six dimensions:
   - Requirement coverage: does the plan solve the core problem without unnecessary scope?
   - Logic completeness: are normal, boundary, and failure paths covered?
   - Code compatibility: does it fit existing architecture and reuse available code?
   - Technical choice: are dependencies, abstractions, and data shapes justified?
   - Verifiability: are success criteria and test scenarios executable?
   - Implementation path: is the sequence short, safe, and realistically sized?

4. Decide the conclusion:
   - Pass: no high-risk issue; proceed.
   - Pass after adjustment: medium issues need edits but no re-review.
   - Redesign required: core requirement, architecture, or risk problem blocks implementation.

5. Save review notes:
   - Write `docs/features/<feature-name>/review_notes.md` when the human has asked you to persist the review.
   - If not writing files in the current environment, provide the complete markdown content.

## Output Shape

```markdown
# Design Review: <feature-name>

## Summary
- Conclusion: Pass | Pass after adjustment | Redesign required
- Reason:

## Strengths
- ...

## Findings
| Severity | Area | Finding | Recommendation |
|----------|------|---------|----------------|

## Six-Dimension Checklist
| Dimension | Result | Notes |
|-----------|--------|-------|

## Required Design Changes
- ...

## Open Discussion
- ...
```

## Severity Guidance

- High: core goal cannot be met, security/privacy issue, severe architecture mismatch, unverifiable design.
- Medium: likely implementation risk, missing edge cases, unclear contracts, avoidable complexity.
- Low: clarity, naming, sequencing, or optional simplification.

## Memory update candidates

Only include this section when a finding is likely to help future, unrelated work in the same project.

```markdown
## Memory update candidates

These are suggestions only. Do not write them to `AGENTS.md` or `CLAUDE.md` unless the human explicitly asks.

- [category] [candidate]: [why it may be reusable]
```

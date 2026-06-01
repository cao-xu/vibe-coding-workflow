# SDD Workflow Skills

[![skills.sh](https://skills.sh/b/cao-xu/vibe-coding-workflow)](https://skills.sh/cao-xu/vibe-coding-workflow)

AI-assisted SDD workflow skills for Codex, Claude Code, and other agents that support the open Agent Skills format.

This repository publishes only the four workflow steps that benefit most from reusable skill guidance. The broader development method still includes implementation, test execution, documentation, and human-controlled knowledge capture; those steps are intentionally handled by humans or normal agents instead of separate skills here.

## Published Skills

| Skill | Purpose | Main Output |
|-------|---------|-------------|
| `design` | Clarify requirements, inspect the repository, and create the technical design | `docs/features/<feature-name>/design.md`, `todo.md` |
| `review` | Independently review a technical design before implementation | `review_notes.md` |
| `test-design` | Design high-ROI tests from requirements and design before coding | `test_design.md` |
| `code-review` | Review code changes in two phases: code quality first, then design compliance | `code_review.md` |

## Install

Install every skill for Codex and Claude Code:

```bash
npx skills add cao-xu/vibe-coding-workflow --skill '*' -a codex -a claude-code
```

Install one skill:

```bash
npx skills add cao-xu/vibe-coding-workflow --skill design
```

List available skills:

```bash
npx skills add cao-xu/vibe-coding-workflow --list
```

Full GitHub URL works as well:

```bash
npx skills add https://github.com/cao-xu/vibe-coding-workflow --skill design
```

## Workflow

Recommended flow:

```text
requirement -> design -> review -> test-design -> implementation -> test execution -> code-review -> documentation
```

Only `design`, `review`, `test-design`, and `code-review` are packaged as skills. Implementation and test execution remain project-specific work, because they depend heavily on the codebase, runtime, environment, and human judgment.

## Documentation Layout

Each feature should keep its working documents under:

```text
docs/features/<feature-name>/
├── design.md
├── todo.md
├── review_notes.md
├── test_design.md
└── code_review.md
```

Use kebab-case for `<feature-name>`, such as `user-auth` or `chat-streaming`.

## Memory Files

Skills may read project memory files when present:

| Agent | File |
|-------|------|
| Codex | `AGENTS.md` |
| Claude Code | `CLAUDE.md` |

Skills in this repository do not automatically edit those files. When a reusable lesson may be worth preserving, the skill outputs a `Memory update candidates` section. A human decides whether to write any candidate into `AGENTS.md` or `CLAUDE.md`.

## Removed Legacy Entry Points

The previous command-style entry points have been removed. This repository is now a pure Agent Skills package with no compatibility layer for the old command files.

## License

[MIT](LICENSE)

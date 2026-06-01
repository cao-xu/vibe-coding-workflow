# SDD 工作流 Skills

[![skills.sh](https://www.skills.sh/b/cao-xu/vibe-coding-workflow)](https://www.skills.sh/cao-xu/vibe-coding-workflow)

面向 Codex、Claude Code 以及其他支持 Agent Skills 格式的 SDD（Spec-Driven Development，规范驱动开发）工作流 skills。

这个仓库只发布最适合沉淀成可复用 skill 的 4 个环节。完整开发工作流仍然包含实现、测试执行、文档整理和经验沉淀等步骤；这些步骤更依赖具体项目、运行环境和人的判断，因此不在本仓库中单独做成 skill。

## 已发布 Skills

| Skill | 用途 | 主要产物 |
|-------|------|----------|
| `design` | 澄清需求、调研仓库、输出技术方案 | `docs/features/<feature-name>/design.md`、`todo.md` |
| `review` | 在实现前独立评审技术方案 | `review_notes.md` |
| `test-design` | 基于需求和方案设计高 ROI 测试 | `test_design.md` |
| `code-review` | 两阶段代码评审：先看代码质量，再看设计符合度 | `code_review.md` |

## 安装

为 Codex 和 Claude Code 安装全部 skills：

```bash
npx skills add cao-xu/vibe-coding-workflow --skill '*' -a codex -a claude-code
```

只安装一个 skill：

```bash
npx skills add cao-xu/vibe-coding-workflow --skill design
```

查看可用 skills：

```bash
npx skills add cao-xu/vibe-coding-workflow --list
```

也可以使用完整 GitHub URL：

```bash
npx skills add https://github.com/cao-xu/vibe-coding-workflow --skill design
```

## 工作流定位

推荐流程：

```text
需求 -> design -> review -> test-design -> 实现 -> 测试执行 -> code-review -> 文档整理
```

只有 `design`、`review`、`test-design`、`code-review` 被打包成 skills。这不代表完整工作流只有 4 步，而是因为这 4 个环节最适合作为跨项目、跨 Agent 复用的流程知识。

实现、测试执行、文档整理仍然是完整工作流的一部分，但它们应由人或普通 agent 根据具体项目执行。

## 文档结构

每个功能建议使用独立目录保存过程文档：

```text
docs/features/<feature-name>/
├── design.md
├── todo.md
├── review_notes.md
├── test_design.md
└── code_review.md
```

`<feature-name>` 使用 kebab-case，例如 `user-auth`、`chat-streaming`。

## 项目记忆文件

Skills 可以读取项目记忆文件作为上下文：

| Agent | File |
|-------|------|
| Codex | `AGENTS.md` |
| Claude Code | `CLAUDE.md` |

本仓库的 skills 不会自动修改这些文件。如果某条经验可能值得沉淀，skill 会输出 `Memory update candidates` 候选项，由人决定是否写入 `AGENTS.md` 或 `CLAUDE.md`。

## 旧入口说明

旧的 slash command 入口已经删除。本仓库现在是纯 Agent Skills 包，不再保留旧命令文件的兼容层。

## License

[MIT](LICENSE)

# SDD 工作流 Skills

[![skills.sh ready](https://img.shields.io/badge/skills.sh-ready-22c55e?labelColor=15803d)](https://www.skills.sh/)

面向 Codex、Claude Code 以及其他支持 Agent Skills 格式的 SDD（Spec-Driven Development，规范驱动开发）工作流 skills。

这个仓库以 SDD 工作流 skills 为主体：只把最适合沉淀成可复用 skill 的 4 个流程环节发布出来。完整开发工作流仍然包含实现、测试执行、文档整理和经验沉淀等步骤；这些步骤更依赖具体项目、运行环境和人的判断，因此不在本仓库中单独做成 skill。

同时，本仓库也收录一个通用辅助 skill：`optdef`（OptDef，优定），用于在正式回答前优化问题定义和答案要求。

## SDD 工作流 Skills

| Skill | 用途 | 主要产物 |
|-------|------|----------|
| [`design`](skills/design/SKILL.md) | 澄清需求、调研仓库、输出技术方案 | `docs/features/<feature-name>/design.md`、`todo.md` |
| [`review`](skills/review/SKILL.md) | 在实现前独立评审技术方案 | `review_notes.md` |
| [`test-design`](skills/test-design/SKILL.md) | 基于需求和方案设计高 ROI 测试 | `test_design.md` |
| [`code-review`](skills/code-review/SKILL.md) | 两阶段代码评审：先看代码质量，再看设计符合度 | `code_review.md` |

## 通用 Skills

| Skill | 用途 | 主要产物 |
|-------|------|----------|
| [`optdef`](skills/optdef/SKILL.md)（OptDef，优定） | 先反问澄清，再把模糊问题整理为结构化的问题定义和答案要求 | 问题定义、答案要求、待确认事项 |

## 安装

为 Codex 和 Claude Code 安装仓库内全部 skills：

```bash
npx skills add cao-xu/sdd-workflow-skills --skill '*' -a codex -a claude-code
```

只安装一个 skill：

```bash
npx skills add cao-xu/sdd-workflow-skills --skill design
```

安装 OptDef（优定）：

```bash
npx skills add cao-xu/sdd-workflow-skills --skill optdef
```

查看可用 skills：

```bash
npx skills add cao-xu/sdd-workflow-skills --list
```

也可以使用完整 GitHub URL：

```bash
npx skills add https://github.com/cao-xu/sdd-workflow-skills --skill design
```

当前仓库已经按 skills CLI 支持的 GitHub repo 格式组织。若 skills.sh 网页详情页暂时没有索引到新仓库名，以 `npx skills add` 的发现和安装结果为准。

Skills.sh 生态入口：[skills.sh](https://www.skills.sh/)。当前单个 skill 详情页仍可能返回 404；安装与发现请以 `npx skills add cao-xu/sdd-workflow-skills --list` 为准。

## 工作流定位

推荐流程：

```text
需求 -> design -> review -> test-design -> 实现 -> 测试执行 -> code-review -> 文档整理
```

只有 `design`、`review`、`test-design`、`code-review` 被打包成 SDD 工作流 skills。这不代表完整工作流只有 4 步，而是因为这 4 个环节最适合作为跨项目、跨 Agent 复用的流程知识。

实现、测试执行、文档整理仍然是完整工作流的一部分，但它们应由人或普通 agent 根据具体项目执行。

`optdef`（OptDef，优定）不是 SDD 流程步骤，而是通用的问题定义优化器。它适合在任何模糊请求、写作任务、研究问题、产品需求或 prompt 设计之前使用，先把“问题是什么”和“答案要满足什么标准”澄清出来。

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

`docs/features/<feature-name>/` 是 SDD 工作流文档目录。`optdef` 通常不需要写入该目录，除非用户明确希望把澄清后的问题定义沉淀到某个功能文档中。

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

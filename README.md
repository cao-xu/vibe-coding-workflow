# vibe-coding-workflow

> AI 辅助开发的结构化工作流 — 7 个命令覆盖从需求设计到开发闭环的完整流程
>
> Structured AI-assisted dev workflow — 7 slash commands from design to delivery

## 工作流总览 / Workflow Overview

```
/design → /review → /test-design → /dev → /test-run → /code-review → /doc-finish
```

| 阶段 Phase | 命令 Command | 说明 Description |
|------------|-------------|------------------|
| 需求澄清与方案设计 | `/design` | 深度调研、反问确认、输出技术方案和 TODO |
| 技术方案评审 | `/review` | 六维度独立评审，输出评审报告与改进建议 |
| 测试方案设计 | `/test-design` | 测试先行，基于需求和方案设计测试用例与脚本 |
| 开发执行 | `/dev` | 严格按 design.md 实现，最小改动，问题上报 |
| 测试执行 | `/test-run` | 运行测试脚本、分析结果、修复重测、更新文档 |
| 代码评审 | `/code-review` | 两阶段独立审查：代码质量 + 设计符合度 |
| 文档整理 | `/doc-finish` | 生成 changelog、评估知识沉淀、开发闭环 |

## 核心理念 / Core Philosophy

- **方案先行**：需求 → 方案 → 评审 → 测试设计 → 开发 → 测试 → 评审 → 文档
- **上下文隔离**：评审和开发使用独立上下文，保持"运动员/裁判分离"
- **知识沉淀**：每个环节都将高价值经验沉淀到项目记忆文件
- **最小改动**：开发阶段效率第一，严格按方案实现

## 安装 / Installation

### Claude Code

```bash
# 方式 1：通过 Claude Code Plugin 安装（推荐）
claude plugin add vibe-coding-workflow

# 方式 2：手动安装
# 将 commands/ 目录下的 .md 文件复制到 ~/.claude/commands/
cp commands/*.md ~/.claude/commands/
```

安装后即可在 Claude Code 中使用 `/design`、`/review` 等命令。

### OpenAI Codex（AGENTS.md 兼容）

本工作流同时兼容 OpenAI Codex。将 `commands/` 目录下的文件复制到你的项目中即可使用。

所有命令文件中的 `CLAUDE.md / AGENTS.md` 引用会根据你的环境自动适配：
- Claude Code 环境使用 `CLAUDE.md`
- OpenAI Codex 环境使用 `AGENTS.md`

## 项目记忆文件 / AI Memory File

工作流中频繁引用的"项目记忆文件"是指项目根目录下的 AI 配置/记忆文件：

| 环境 Environment | 文件 File | 用途 Purpose |
|------------------|----------|-------------|
| Claude Code | `CLAUDE.md` | 项目约定、经验沉淀、避坑指南 |
| OpenAI Codex | `AGENTS.md` | 同上 |

工作流会在设计、开发、测试、评审等环节自动读取和更新该文件。

## 使用示例 / Usage Example

### 典型开发流程

```bash
# 1. 需求分析与方案设计
/design 新功能 实现用户认证模块，支持 JWT token

# 2. 方案独立评审（新的对话上下文）
/review user-auth

# 3. 测试方案设计（新的对话上下文）
/test-design user-auth

# 4. 开发执行
/dev user-auth

# 5. 测试执行
/test-run user-auth

# 6. 代码评审（新的对话上下文）
/code-review user-auth main..feature/user-auth

# 7. 文档整理
/doc-finish user-auth main..feature/user-auth
```

### 文档结构

每个功能模块会生成以下文档：

```
docs/features/<feature-name>/
├── design.md          # 技术方案（/design 输出）
├── todo.md            # 工作计划（/design 输出）
├── review_notes.md    # 评审记录（/review 输出）
├── test_design.md     # 测试设计（/test-design 输出）
├── code_review.md     # 代码评审报告（/code-review 输出）
└── changelog.md       # 变更日志（/doc-finish 输出）
```

## 自定义 / Customization

每个命令文件底部都有 **「扩展规则」** 区域，你可以根据项目需要添加：

- **项目特定约定**：命名规范、架构约束
- **技术约束**：依赖限制、环境要求
- **评审重点**：特别需要关注的代码模式
- **测试场景**：项目特有的测试要求

例如，`test-design.md` 底部的「项目背景」区域提供了注释模板：

```markdown
<!-- ## 项目信息 -->
<!-- - 项目类型：FastAPI 后端服务 -->
<!-- - 技术特点：SSE 流式响应 -->
<!-- - 测试环境：本地启动，无需鉴权 -->
<!-- - 环境配置：.env 文件控制 -->
```

取消注释并填写你的项目信息即可。

## 命令详细说明 / Command Details

### `/design` — 需求澄清与技术方案设计

角色：资深软件架构师。通过深度调研 → 反问确认 → 输出方案 → 生成文档四个步骤，产出完整的技术方案和 TODO 清单。支持快速模式（小需求跳过深度调研）。

### `/review` — 技术方案独立评审

角色：独立技术评审者。从需求覆盖、逻辑完整、代码兼容、技术选型、可验证性、实现路径六个维度审查方案。支持双向评论直到达成共识。

### `/test-design` — 测试方案设计

角色：QA 工程师。基于 ROI 原则决定单元测试 vs E2E 测试策略，生成完整的测试脚本和测试设计文档。测试先行，基于需求而非代码。

### `/dev` — 开发执行

角色：执行者。严格按 design.md 实现，最小改动原则。支持单任务和并行开发两种模式。遇到问题暂停上报，不擅自决策。

### `/test-run` — 测试执行

角色：测试执行者。按顺序运行单元测试 → 功能测试 → 回归测试，分析失败原因，记录执行日志。

### `/code-review` — 代码评审

角色：独立评审者。第一阶段纯代码视角评审质量，第二阶段对照 design.md 检查设计符合度。问题分级（Blocker/Major/Minor/Good），双向评论直到共识。

### `/doc-finish` — 文档整理

角色：文档整理者。生成 Feature Changelog，评估知识沉淀，检查 TODO 完成情况，为本次开发画上句号。

## License

[MIT](LICENSE)

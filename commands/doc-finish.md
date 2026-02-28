---
description: 文档整理（生成 changelog、评估知识沉淀、检查 todo 完成、开发闭环）
allowed-tools: Read(*), Write(*), Bash(find:*), Bash(cat:*), Bash(ls:*), Bash(grep:*), Bash(git:*), Bash(mkdir:*)
argument-hint: [功能模块名 kebab-case] [commit范围，如 main..feature-branch]
model: opus
---

> **环境兼容说明：** 本文档中的 `CLAUDE.md / AGENTS.md` 指项目根目录下的 AI 记忆文件。
> - Claude Code → `CLAUDE.md`
> - OpenAI Codex → `AGENTS.md`
> 请根据你所在的环境使用对应的文件。

# 文档整理（开发闭环）

## 本环节定位

```
1. 需求分析与评审
       ↓
2. 开发方案设计 → todo.md, design.md
       ↓
3. 开发方案评审（非必须，独立上下文）
       ↓
4. 测试方案设计 → test_design.md
       ↓
5. 测试方案评审（非必须，独立上下文）
       ↓
6. 测试基础设施准备（非必须）
       ↓
7. 开发执行 → 代码实现
       ↓
8. 测试执行
       ↓
9. 代码评审 → code_review.md
       ↓
10. 【文档整理】← 当前环节（最后一步）
```

## 进入本环节的前提条件

- ✅ 代码评审已通过
- ✅ `code_review.md` 已生成
- ✅ 代码已提交到 Git

## 工程师的职责

1. **提供本次功能的模块名称**：用于定位文档目录
2. **提供相关的 commit 信息**：用于生成 changelog
3. **确认知识库更新内容**：AI 只能建议，工程师确认后才写入
4. **确认 CLAUDE.md / AGENTS.md 更新内容**：项目级约定需要工程师确认

---

# AI 执行指令

## AI 角色定位

- 📝 **文档整理者**：汇总本次开发的所有产出，生成 changelog
- 🔍 **经验提取者**：从开发过程中提取值得沉淀的经验
- ⚠️ **建议者而非决策者**：知识库更新必须经过工程师确认

## AI 执行原则

### 原则 1：完整闭环

确保本次开发的所有产出都被妥善记录，为这次开发画上完整的句号。

### 原则 2：精选沉淀

知识库只收录真正有价值的经验教训，不堆砌信息。

**沉淀前自问：**
- 这个经验会在其他功能开发中遇到吗？
- 6个月后做类似功能时，这条信息还有用吗？
- 这是项目级的约定或工具使用方式吗？

### 原则 3：必须确认

任何 `CLAUDE.md / AGENTS.md` 的更新都必须经过工程师确认，AI 不能自作主张写入。

---

# AI 工作流程

## Step 0: 确认功能模块

```
## 文档整理开始

请工程师提供以下信息：
1. 本次功能的模块名称（kebab-case）
2. 相关的 commit（hash 或范围，用于生成 changelog）
```

**功能模块名称和 commit 范围从 $ARGUMENTS 获取（格式：`模块名 commit范围`），如果未提供，必须先询问我。**

**等待工程师提供信息。**

---

## Step 1: 阅读本次开发的所有材料

### 1.1 获取 commit 变更

```
# 查看相关 commit 的变更内容
git show <commit-hash>
# 或
git log --oneline -n 5
git diff <start-hash>..<end-hash>
```

### 1.2 阅读功能文档

按顺序阅读 `docs/features/<feature-name>/` 下的文档：

| 文档 | 获取的信息 |
|------|-----------|
| `design.md` | 需求目标、技术方案 |
| `todo.md` | 任务完成情况 |
| `review_notes.md`（如有） | 方案评审中的问题和决策 |
| `test_design.md` | 测试策略、测试结论 |
| `code_review.md` | 代码评审结论、改进点 |

### 1.3 阅读项目记忆

阅读 `CLAUDE.md / AGENTS.md` 了解项目约定和已有的经验沉淀，避免重复记录。

---

## Step 2: 生成 Feature Changelog

在 `docs/features/<feature-name>/` 下创建 `changelog.md`：

```
# Feature Changelog: <feature-name>

## 基本信息
- **完成日期：** YYYY-MM-DD
- **关联 commit：** [commit hash 或范围]

## 需求目标
[一句话描述这个功能要解决什么问题]

## 方案简述
[2-3 句话概括技术方案的核心思路]

## 变更内容

### Added
- [新增的功能/文件]

### Changed
- [修改的功能/文件]

### Fixed
- [修复的问题]

## 测试结论
- **功能测试：** ✅ 通过 / ❌ 未通过
- **回归测试：** ✅ 通过 / ❌ 未通过

## 代码评审结论
- **评审结果：** ✅ 通过
- **主要改进点：** [列出]
```

---

## Step 3: 评估 CLAUDE.md / AGENTS.md 更新（必须反问确认）

从以下材料中提取**可能值得沉淀的经验**：
- `review_notes.md` 中的重要评审意见
- `code_review.md` 中的代码改进经验
- 开发过程中踩过的坑

**然后向工程师确认：**

```
## CLAUDE.md / AGENTS.md 更新建议

我从本次开发中提取了以下可能值得沉淀的经验：

### 候选 1：[标题]
- **来源：** [哪个文档/什么场景]
- **内容摘要：** [简述]
- **类型：** [项目约定 / 工具使用 / 踩坑记录]

### 候选 2：[标题]
- ...

### 无候选经验
（如果没有值得沉淀的内容，说明原因）

---

请工程师确认：
1. 以上哪些内容需要写入 CLAUDE.md / AGENTS.md？（输入序号，如 "1, 2" 或 "无"）
2. 是否需要调整内容？
```

**等待工程师确认后，再执行写入。**

---

## Step 4: 更新 CLAUDE.md / AGENTS.md（确认后执行）

根据工程师确认的内容，追加到 `CLAUDE.md / AGENTS.md`：

```
## 经验沉淀：<feature-name>（YYYY-MM-DD）

### [经验类型]
- [经验内容]：[说明]
```

**格式要求：**
- 每条经验不超过 2 行
- 标注来源功能和日期
- 归类到合适的类型下（项目约定 / 工具使用 / 踩坑记录）

---

## Step 5: 检查 todo.md 完成情况

确认 `todo.md` 中的所有任务都已完成：

```
## todo.md 检查

### 任务完成情况
- [x] 任务1 ✅
- [x] 任务2 ✅
- [ ] 任务3 ⚠️ 未完成

### 未完成任务处理（如果有）
- [任务3]：[原因] → [后续计划]
```

如果有未完成的任务，向工程师确认处理方式。

---

## Step 6: 输出工作总结

```
## ✅ 文档整理完成

### 本次生成/更新的文件
| 文件 | 状态 |
|------|------|
| `docs/features/<feature-name>/changelog.md` | ✅ 已创建 |
| `CLAUDE.md / AGENTS.md` | [✅ 已更新 / ➖ 无需更新] |

### 检查结果
- **todo.md 任务：** [全部完成 / 有遗留]
- **文档完整性：** [完整 / 缺失 xxx]

### 本次开发闭环
功能 `<feature-name>` 开发完成，所有文档已整理完毕。
```

---

# 职责边界总结

## AI 的职责
- ✅ 阅读 commit 和功能文档，生成 changelog
- ✅ 提取值得沉淀的经验，向工程师建议
- ✅ 确认后更新 CLAUDE.md / AGENTS.md
- ✅ 检查 todo.md 完成情况
- ❌ 不要未经确认就写入 CLAUDE.md / AGENTS.md
- ❌ 不要堆砌无价值的信息

## 工程师的职责
- ✅ 提供功能模块名称和 commit 信息
- ✅ 确认 CLAUDE.md / AGENTS.md 更新内容
- ✅ 处理未完成的任务

---

# 项目文档体系

```
项目根目录/
├── CLAUDE.md / AGENTS.md                  # 项目级约定、工具使用、经验沉淀
└── docs/
    └── features/
        └── <feature-name>/
            ├── design.md              # 需求分析与方案设计
            ├── todo.md                # 任务列表
            ├── review_notes.md        # 方案评审意见（如有）
            ├── test_design.md         # 测试方案设计
            ├── code_review.md         # 代码评审报告
            └── changelog.md           # 功能变更日志（本环节生成）
```

---

# 扩展规则（持续更新）

## CLAUDE.md / AGENTS.md 沉淀分类
-

## 额外需要整理的内容
-

## 特殊约定
-

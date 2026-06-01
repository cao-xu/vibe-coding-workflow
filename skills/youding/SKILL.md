---
name: youding
description: Use when a user wants to clarify, scope, refine, or optimize an ambiguous question, request, prompt, answer requirement, writing task, research topic, or decision problem before getting the final answer; especially when they mention 优定, 问题定义, 答案要求, 需求澄清, or problem definition.
---

# 优定：问题定义优化器

## Overview

优定把模糊、不完整或过宽的问题，转化为清晰、结构化、可执行的问题定义和答案要求。

This is a clarification skill, not a direct-answer skill. The goal is to define the problem before solving it.

## Core Rules

- Must ask the user at least one clarification round before producing the final problem definition.
- Do not answer the substantive question during the clarification round.
- Analyze two things in every request:
  - What is the actual problem?
  - What kind of answer does the user expect?
- Ask targeted questions about context, scope, required depth, included/excluded content, output format, and quality bar.
- If the request already looks clear, still ask at least one confirmation question about scope or answer criteria.
- Keep each clarification round compact: usually 3-7 questions.
- After the user replies, produce the structured definition. If key information is still missing, ask one more focused round before finalizing.
- If the user refuses to add detail after at least one clarification round, produce a "provisional definition" and list assumptions.

## First Response Shape

Use this shape before producing any final definition:

```markdown
我先用一轮问题把需求收束清楚。

关于问题本身：
- ...
- ...

关于答案要求：
- ...
- ...
```

Question prompts should be specific to the user's input. Avoid generic questionnaires when the user's topic provides enough signal.

## Final Output Shape

After the user answers at least one clarification round, use:

```markdown
根据你的补充，我把需求重新定义如下：

## 问题定义

1. 核心问题陈述：
   - ...

2. 关键上下文信息：
   - ...

3. 具体范围界定：
   - 包含：
   - 不包含：

## 答案要求

1. 内容范围：
   - 必须包含：
   - 不应包含：

2. 深度要求：
   - ...

3. 形式要求：
   - ...

4. 质量标准：
   - ...

## 待确认

- 这个定义是否准确反映你的需求？
- 哪些范围或答案要求还需要调整？
```

## Handling Common Cases

- Writing requests: clarify audience, purpose, length, tone, examples/data needs, and publication channel.
- Research requests: clarify time range, sources, evidence standard, geographic/domain scope, and expected conclusion type.
- Product or engineering requests: clarify user scenario, constraints, acceptance criteria, out-of-scope items, and delivery format.
- Decision requests: clarify options, decision criteria, constraints, risk tolerance, and desired recommendation style.
- Prompt requests: clarify target model/agent, input variables, output format, failure modes, and examples.

## What Not To Do

- Do not skip the clarification round.
- Do not produce the final definition from the original input alone.
- Do not turn the skill into a full solution, article, plan, or code implementation.
- Do not ask excessive questions when a small number of high-signal questions will unlock the definition.

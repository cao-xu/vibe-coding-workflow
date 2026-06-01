# 变更日志

## 未发布

### 变更

- 将仓库从 Claude slash-command 插件迁移为纯 Agent Skills 包。
- 将公开仓库入口更新为 `cao-xu/sdd-workflow-skills`。
- 发布 4 个 SDD 工作流 skills：
  - `design`
  - `review`
  - `test-design`
  - `code-review`
- 新增通用问题定义优化 skill：
  - `youding`（优定）
- 更新 `README.md`，说明 `npx skills add` 和 skills.sh 安装方式。
- 将 README 中暂不可用的 skills.sh 官方图片 badge 和详情页链接，改为稳定的静态 badge，并链接仓库内的 `SKILL.md` 文件。
- 在 README 安装说明中补充轻量的 skills.sh 生态入口和单个 skill 页面链接。

### 删除

- 删除 `commands/` 下的旧 slash command 文件。
- 删除 `.claude-plugin/plugin.json`。
- 删除低频命令工作流：
  - `/dev`
  - `/test-run`
  - `/doc-finish`

### 行为变化

- Skills 可以读取 `AGENTS.md` 或 `CLAUDE.md` 作为项目上下文。
- Skills 不再自动更新 `AGENTS.md` 或 `CLAUDE.md`。
- 可复用经验改为输出 `Memory update candidates`，由人决定是否写入项目记忆文件。

### 迁移方式

使用以下命令安装新的 skills：

```bash
npx skills add cao-xu/sdd-workflow-skills --skill '*' -a codex -a claude-code
```

旧 slash commands 不再支持。

### 验证

- `find skills -name SKILL.md -print | sort`
- 校验 5 个 skills 的 YAML frontmatter
- `npx --yes skills add ./ --list`
- 使用临时目录执行安装测试：`npx --yes skills add <local-repo> --skill '*' -a codex -a claude-code -y --copy`

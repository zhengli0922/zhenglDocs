---
title: Claude Code最佳实践完全指南
date: 2026-03-23
tags: [Claude, AI编程]
source: https://github.com/shanraisshan/claude-code-best-practice
type: knowledge
---
# Claude Code 最佳实践完全指南（完整版）

> 来源：https://github.com/shanraisshan/claude-code-best-practice
> Star: 20.7k | Fork: 1.8k
> 更新时间：2026-03-23
> 标签：#ClaudeCode #AI编程 #最佳实践

---

## 🧠 核心概念

### 三大核心组件

| 组件 | 文件位置 | 作用 |
|------|---------|------|
| **Subagents** | `.claude/agents/<name>.md` | 独立隔离的 Agent，有自定义工具、权限、模型、记忆 |
| **Commands** | `.claude/commands/<name>.md` | 用户调用的提示词模板，用于工作流编排 |
| **Skills** | `.claude/skills/<name>/SKILL.md` | 可配置、可预加载、自动发现的知识模块 |

**符号说明**：🤖 = Agents | ⌨️ = Commands | 📚 = Skills

### 编排模式
```
Command → Agent → Skill
```

---

## 🤖 Subagents 详解

### Frontmatter 字段（15个）

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `name` | string | ✅ | 唯一标识符，小写字母+连字符 |
| `description` | string | ✅ | 何时调用，用 `"PROACTIVELY"` 启用自动调用 |
| `tools` | string/list | ❌ | 工具白名单（如 `Read, Write, Edit, Bash`），省略则继承所有 |
| `disallowedTools` | string/list | ❌ | 工具黑名单 |
| `model` | string | ❌ | 模型别名：`haiku`, `sonnet`, `opus`, `inherit` |
| `permissionMode` | string | ❌ | 权限模式：`default`, `acceptEdits`, `dontAsk`, `bypassPermissions`, `plan` |
| `maxTurns` | integer | ❌ | 最大 Agent 轮数 |
| `skills` | list | ❌ | 预加载到 Agent 上下文的 Skill 名称 |
| `mcpServers` | list | ❌ | MCP 服务器配置 |
| `hooks` | object | ❌ | 生命周期钩子 |
| `memory` | string | ❌ | 持久化内存范围：`user`, `project`, `local` |
| `background` | boolean | ❌ | 设为 `true` 则始终后台运行 |
| `effort` | string | ❌ | 努力级别：`low`, `medium`, `high`, `max` |
| `isolation` | string | ❌ | 设为 `"worktree"` 则在临时 git worktree 中运行 |
| `color` | string | ❌ | CLI 输出颜色 |

### 官方内置 Agent（6个）

| Agent | 模型 | 工具 | 用途 |
|-------|------|------|------|
| `general-purpose` | inherit | 全部 | 复杂多步骤任务（默认） |
| `Explore` | haiku | 只读 | 快速代码库搜索和探索 |
| `Plan` | inherit | 只读 | 计划模式预规划研究 |
| `Bash` | inherit | Bash | 在独立上下文中运行终端命令 |
| `statusline-setup` | sonnet | Read, Edit | 配置状态栏 |
| `claude-code-guide` | haiku | Glob, Grep, Read, WebFetch, WebSearch | 回答 Claude Code 功能问题 |

---

## ⌨️ Commands 详解

### Frontmatter 字段（11个）

| 字段 | 类型 | 必填 | 说明 |
|------|------|------|------|
| `name` | string | ❌ | 显示名称和 `/slash-command` 标识符 |
| `description` | string | 推荐 | 命令描述，用于自动发现 |
| `argument-hint` | string | ❌ | 自动补全提示（如 `[issue-number]`） |
| `disable-model-invocation` | boolean | ❌ | 设为 `true` 阻止 Claude 自动调用 |
| `user-invocable` | boolean | ❌ | 设为 `false` 从 `/` 菜单隐藏 |
| `allowed-tools` | string | ❌ | 允许的工具（无权限提示） |
| `model` | string | ❌ | 模型别名 |
| `effort` | string | ❌ | 努力级别覆盖 |
| `context` | string | ❌ | 设为 `fork` 在隔离子 Agent 上下文运行 |
| `agent` | string | ❌ | `context: fork` 时的子 Agent 类型 |
| `hooks` | object | ❌ | 生命周期钩子 |

### 官方内置命令（63个）

#### 🔐 认证相关
- `/login` - OAuth 登录
- `/logout` - 登出
- `/upgrade` - 升级计划

#### ⚙️ 配置相关
- `/config` 或 `/settings` - 打开设置界面
- `/permissions` 或 `/allowed-tools` - 查看/更新工具权限
- `/theme` - 更改颜色主题
- `/vim` - 启用 vim 编辑模式
- `/voice` - 切换语音输入
- `/keybindings` - 自定义快捷键

#### 📊 上下文相关
- `/context` - 可视化当前上下文使用情况
- `/cost` - 显示 token 使用统计
- `/stats` - 可视化每日使用量
- `/status` - 显示版本、模型、账户信息

#### 🔧 调试相关
- `/doctor` - 检查 Claude Code 安装健康状况
- `/feedback` 或 `/bug` - 生成 GitHub issue URL
- `/help` - 显示帮助
- `/tasks` - 列出后台任务

#### 📁 项目相关
- `/init` - 初始化项目 CLAUDE.md
- `/diff` - 打开差异查看器
- `/pr-comments` - 审查或回复 PR 评论
- `/security-review` - 运行安全审查

#### 🔄 会话相关
- `/clear` 或 `/reset` - 清除对话历史
- `/compact` - 压缩对话释放上下文
- `/rewind` 或 `/checkpoint` - 回滚对话
- `/fork` 或 `/branch` - 分叉当前会话
- `/resume` 或 `/continue` - 恢复之前的会话

#### 🚀 扩展相关
- `/agents` - 管理自定义子 Agent
- `/hooks` - 管理钩子配置
- `/mcp` - 管理 MCP 服务器
- `/plugin` - 管理插件
- `/skills` - 列出可用技能

---

## 📚 Skills 详解

### Frontmatter 字段（11个）

与 Commands 相同，但 `user-invocable: false` 时 Skill 变为后台知识，仅供 Agent 预加载。

### 官方内置 Skills（5个）

| Skill | 用途 |
|-------|------|
| `simplify` | 审查代码的复用性、质量、效率，重构消除重复 |
| `batch` | 批量跨多个文件运行命令 |
| `debug` | 调试失败的命令或代码问题 |
| `loop` | 定期运行提示词或命令（最长3天） |
| `claude-api` | 构建 Claude API 应用 |

### 9 种 Skill 类型

| 类型 | 用途 | 示例 |
|------|------|------|
| **Library & API Reference** | 解释如何正确使用库/CLI/SDK | billing-lib, frontend-design |
| **Product Verification** | 测试或验证代码 | signup-flow-driver, checkout-verifier |
| **Data Fetching & Analysis** | 连接数据和监控栈 | funnel-query, grafana |
| **Business Process & Team Automation** | 自动化重复工作流 | standup-post, weekly-recap |
| **Code Scaffolding & Templates** | 生成框架样板代码 | new-migration, create-app |
| **Code Quality & Review** | 执行代码质量标准 | adversarial-review, code-style |
| **CI/CD & Deployment** | 获取、推送、部署代码 | babysit-pr, deploy-service |
| **Runbooks** | 多工具调查，生成报告 | service-debugging, oncall-runner |
| **Infrastructure Operations** | 例行维护和操作程序 | resource-orphans, cost-investigation |

### Skill 编写技巧

1. **不要陈述显而易见的事** - Claude 已知很多，聚焦于独特信息
2. **建立 Gotchas 部分** - 记录常见失败点
3. **使用文件系统和渐进披露** - Skill 是文件夹，不仅仅是 markdown
4. **避免过度约束 Claude** - 给目标而非步骤
5. **考虑设置流程** - 用 `config.json` 存储配置
6. **Description 字段是给模型看的** - 写何时触发，而非摘要
7. **内存和数据存储** - 用 `${CLAUDE_PLUGIN_DATA}` 存储稳定数据
8. **存储脚本并生成代码** - 让 Claude 聚焦于组合而非重建样板
9. **按需钩子** - `/careful` 阻止危险操作，`/freeze` 冻结目录

---

## 💾 Memory 管理

### CLAUDE.md 加载机制

```
向上加载（Ancestor Loading）: 启动时向上遍历目录树，加载所有 CLAUDE.md
向下加载（Descendant Loading）: 懒加载，仅当访问子目录时才加载
```

### Monorepo 示例

```
/mymonorepo/
├── CLAUDE.md          # 根级（共享）
├── frontend/
│   └── CLAUDE.md      # 前端专用（懒加载）
├── backend/
│   └── CLAUDE.md      # 后端专用（懒加载）
└── api/
    └── CLAUDE.md      # API专用（懒加载）
```

**关键点**：
- 从根目录启动：只加载根 CLAUDE.md
- 从 frontend 启动：加载根 + frontend CLAUDE.md
- 兄弟目录永不互相加载

### 最佳实践

1. **共享约定放根 CLAUDE.md** - 编码标准、提交格式、PR 模板
2. **组件特定放子目录 CLAUDE.md** - 框架模式、架构、测试约定
3. **个人偏好用 CLAUDE.local.md** - 加入 `.gitignore`

---

## 🔥 Boris Cherny 的 13 条技巧

### 1. 并行运行 5 个 Claude
- 终端标签编号 1-5
- 用系统通知知道何时需要输入

### 2. 使用 claude.ai/code 获得更多并行
- 本地 5 个 + 网页 5-10 个

### 3. 所有任务都用 Opus + Thinking
- 虽然 Opus 更大更慢
- 但因为需要引导更少，工具使用更好
- 最终几乎总是比小模型更快

### 4. 与团队共享单个 CLAUDE.md
- 提交到 git
- 团队每周多次贡献
- Claude 做错就加到 CLAUDE.md

### 5. 在 PR 上标记 @claude 更新 CLAUDE.md
- 代码审查时标记 `@claude`
- 让 Claude 作为 PR 的一部分更新 CLAUDE.md

### 6. 大多数会话从 Plan 模式开始
- shift+tab 两次进入 Plan 模式
- 和 Claude 来回讨论计划
- 切换到自动接受编辑模式
- 好计划非常重要

### 7. 用 Slash Commands 处理内循环工作流
- 每天多次重复的工作流用 slash commands
- 保存到 `.claude/commands/`

### 8. 用 Subagents 自动化常见工作流
- `code-simplifier` - Claude 完成后简化代码
- `verify-app` - 端到端测试

### 9. 用 PostToolUse Hook 自动格式化代码
```json
"PostToolUse": [
  {
    "matcher": "Write|Edit",
    "hooks": [{ "type": "command", "command": "bun run format || true" }]
  }
]
```

### 10. 预允许权限而非 --dangerously-skip-permissions
- 用 `/permissions` 预先允许常见安全命令
- 大多数提交到 `.claude/settings.json` 与团队共享

### 11. 让 Claude 通过 MCP 使用所有工具
- Slack MCP - 搜索和发布消息
- BigQuery - 运行查询
- Sentry - 获取错误日志

### 12. 用后台 Agent 验证长时间运行的任务
- (a) 让 Claude 用后台 Agent 验证工作
- (b) 用 Agent Stop 钩子
- (c) 用 ralph-wiggum 插件

### 13. 给 Claude 验证工作的方法（最重要！）
- 如果有反馈循环
- 最终结果质量提高 2-3 倍
- Boris 落地的每个改动都测试

---

## 🔥 热门新功能

### Channels（Beta）
- `--channels` 插件方式
- Telegram、Discord、Webhooks 推送到运行中的会话

### Code Review（Beta）
- GitHub App 托管
- 多 Agent PR 分析，发现 bug、安全漏洞、回归

### Scheduled Tasks
- `/loop` + cron 工具
- 定时执行提示词（最长3天）

### Agent Teams（Beta）
- 多 Agent 并行工作
- 共享任务协调

### Remote Control
- `/remote-control` 或 `/rc`
- 从手机、平板、浏览器继续本地会话

### Git Worktrees
- 隔离的 git 分支
- 每个 Agent 获得独立工作副本

---

## 🛠 热门开发工作流

| 名称 | Star | 特点 |
|------|------|------|
| **Superpowers** | 103k | TDD优先、铁律、全计划审查 |
| **Everything Claude Code** | 93k | 本能评分、AgentShield、多语言规则 |
| **Spec Kit** | 79k | 规范驱动、宪法式、22+工具 |
| **BMAD-METHOD** | 42k | 完整SDLC、Agent角色、22+平台 |
| **Get Shit Done** | 38k | 新鲜200K上下文、波次执行、XML计划 |
| **gstack** | 34k | 角色角色、/codex审查、并行冲刺 |

---

## 📚 相关资源

- 官方文档：https://code.claude.com/docs
- 官方 Skills：https://github.com/anthropics/skills
- 本地仓库：`D:\DevProduct\claude-code-best-practice`

---

*整理：冰淇淋🍦*
*时间：2026-03-23*

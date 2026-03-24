# MCO 项目归档文档

> 本文档是对 GitHub 项目 [mco-org/mco](https://github.com/mco-org/mco) 的深度分析与归档。
>
> 归档日期：2026-03-24

---

## 文档目录

| 文档 | 说明 |
|------|------|
| [01-项目概述.md](./01-项目概述.md) | 项目介绍、核心价值与定位 |
| [02-核心架构.md](./02-核心架构.md) | 系统架构设计、执行流程 |
| [03-功能模块.md](./03-功能模块.md) | 各功能模块详解 |
| [04-内置Provider.md](./04-内置Provider.md) | 支持的 AI Agent 列表 |
| [05-API文档.md](./05-API文档.md) | CLI 命令与参数详解 |
| [06-使用指南.md](./06-使用指南.md) | 安装、配置与使用示例 |
| [07-共识引擎.md](./07-共识引擎.md) | 共识引擎与去重机制 |
| [08-高级特性.md](./08-高级特性.md) | 自定义 Agent、辩论模式等 |

---

## 快速概览

### 项目定位

**MCO（Multi-CLI Orchestrator）** 是一个中立的 AI 编程 Agent 编排层。它将提示词并行分发给多个 Agent CLI，汇总执行结果，返回结构化输出。

### 核心价值

```
一个 Agent 是工具，五个 Agent 是团队
```

- **并行扇出**：同时分发任务到 Claude、Codex、Gemini、OpenCode、Qwen
- **共识引擎**：跨 Agent 去重、共识评分、置信度计算
- **多种输出**：JSON、SARIF、Markdown-PR 格式

### 一行命令示例

```bash
mco review \
  --repo . \
  --prompt "审查此仓库的高风险 Bug 和安全问题" \
  --providers claude,codex,qwen
```

### 技术栈

| 项目 | 说明 |
|------|------|
| 语言 | Python 3.10+ |
| 许可证 | MIT |
| 安装方式 | npm / pip |
| 入口命令 | `mco` |

---

## 项目元信息

```toml
name = "mco"
version = "0.9.1"
description = "Neutral multi-provider CLI orchestrator for agent-style run/review workflows."
requires-python = ">=3.10"
license = "MIT"
```

---

## 相关链接

- **GitHub**: https://github.com/mco-org/mco
- **npm 安装**: `npm i -g @tt-a1i/mco`
- **pip 安装**: `pip install mco`

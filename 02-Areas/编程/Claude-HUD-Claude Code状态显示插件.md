---
title: Claude HUD - Claude Code 状态显示插件
date: 2026-03-24
source: https://github.com/jarrodwatts/claude-hud
author: jarrodwatts
tags: [Claude-Code, 插件, HUD, 状态栏, 工具]
type: area-knowledge
---

# Claude HUD - Claude Code 状态显示插件

> Claude Code 插件，实时显示上下文使用量、工具活动、Subagent状态和Todo进度

## 简介

Claude HUD 利用 Claude Code 原生 statusline API，在终端底部实时展示会话状态信息，无需额外窗口或 tmux。

## 安装

```bash
# 1. 添加marketplace
/plugin marketplace add jarrodwatts/claude-hud

# 2. 安装插件
/plugin install claude-hud

# 3. 配置状态栏
/claude-hud:setup
```

Windows用户需要先安装 Node.js：`winget install OpenJS.NodeJS.LTS`

## 显示内容

| 信息 | 说明 |
|------|------|
| 项目路径 | 当前项目目录+git分支 |
| 上下文健康度 | 实时context window使用率（绿→黄→红） |
| Token数据 | 来自Claude Code原生数据（非估算） |
| 工具活动 | 实时显示文件读取、编辑、搜索操作 |
| Agent状态 | 显示运行中的subagent及任务 |
| Todo进度 | 实时跟踪任务完成情况 |
| 用量限制 | Claude订阅用量（Pro用户默认开启） |
| 会话时长 | 可选显示 |
| 输出速度 | 可选显示 tok/s |

## 配置预设

| 预设 | 说明 |
|------|------|
| Full | 全部开启 — 工具、Agent、Todo、Git、用量、时长 |
| Essential | 活动行+Git状态，最小干扰 |
| Minimal | 仅模型名+上下文条 |

## 自定义配置

配置文件：`~/.claude/plugins/claude-hud/config.json`

主要选项：
- `lineLayout`: expanded（多行）或 compact（单行）
- `pathLevels`: 显示1-3级目录
- `display.contextValue`: percent/tokens/remaining/both
- `display.showTools`: 显示工具活动
- `display.showAgents`: 显示Agent状态
- `display.showTodos`: 显示Todo进度
- 自定义颜色：支持颜色名和256色值

## 技术原理

- 使用 Claude Code 原生 statusline API
- 通过 stdin JSON → claude-hud 处理 → stdout 输出
- 每~300ms更新一次
- 支持最新1M上下文窗口的session

## 配置命令

```bash
/claude-hud:configure  # 引导式配置
/claude-hud:setup      # 首次安装设置
```

## 相关链接

- GitHub: https://github.com/jarrodwatts/claude-hud
- 许可证: MIT

---
title: GSD - Claude Code 规格驱动开发系统
date: 2026-03-24
source: https://github.com/gsd-build/get-shit-done
author: TÂCHES (glittercowboy)
tags: [Claude-Code, 规格驱动开发, 上下文工程, subagent, Meta-Prompting]
type: area-knowledge
---

# GSD (Get Shit Done) - Claude Code 规格驱动开发系统

> 轻量级Meta-Prompting、上下文工程和规格驱动开发系统，支持 Claude Code、OpenCode、Gemini CLI、Codex、Copilot、Antigravity

## 核心理念

解决 **context rot（上下文腐烂）** — Claude填满上下文窗口时质量下降的问题。

GSD 的复杂度在系统内部，不在你的工作流中。底层：上下文工程、XML prompt格式化、subagent编排、状态管理。你看到的：几个命令就能搞定。

## 安装

```bash
npx get-shit-done-cc@latest
```

支持选择运行时（Claude Code/OpenCode/Gemini/Codex/Copilot/Cursor/Antigravity）和安装位置（全局/当前项目）。

非交互式安装：
```bash
npx get-shit-done-cc --claude --global
```

## 核心工作流

### 1. 已有项目：先映射代码库
```
/gsd:map-codebase
```
生成并行agent分析技术栈、架构、约定和关注点。

### 2. 新建项目
```
/gsd:new-project
```
一个命令完成全流程：
- **提问** — 持续追问直到完全理解你的想法
- **调研** — 生成并行agent调研领域知识（推荐）
- **需求** — 提取v1、v2和超出范围的内容
- **路线图** — 创建按需求映射的阶段

生成文件：PROJECT.md、REQUIREMENTS.md、ROADMAP.md、STATE.md、planning/research/

### 3. 讨论阶段
```
/gsd:discuss-phase 1
```
在实现前捕获偏好，确保按你想象的方式构建。

## 推荐用法

```bash
claude --dangerously-skip-permissions
```
或配置细粒度权限到 `.claude/settings.json`（允许git、date等常用命令）。

## 支持平台

| 平台 | 帮助命令 |
|------|---------|
| Claude Code / Gemini | `/gsd:help` |
| OpenCode | `/gsd-help` |
| Codex | `$gsd-help` |
| Copilot | `/gsd:help` |
| Antigravity | `/gsd:help` |

## 适用人群

- 想要描述需求就正确构建的开发者
- 不想假装管理50人工程团队的个人开发者
- 追求简洁高效的创意构建者

## 设计哲学

- 不搞企业级角色扮演（sprint仪式、故事点、Jira流程）
- 让系统理解全局，不丢失大局观
- Context Engineering > 更多Prompt

## 对比其他工具

相比 BMAD、Speckit、Taskmaster 等工具：更简洁、更理解全局、不引入企业级流程。

## 相关链接

- GitHub: https://github.com/gsd-build/get-shit-done
- NPM: https://www.npmjs.com/package/get-shit-done-cc
- Discord: https://discord.gg/gsd
- 许可证: MIT

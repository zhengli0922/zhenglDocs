---
title: Superpowers - AI编程技能框架
date: 2026-03-24
source: https://github.com/obra/superpowers
author: Jesse Vincent (obra)
tags: [Claude-Code, AI编程, 技能框架, TDD, subagent]
type: area-knowledge
---

# Superpowers - AI编程技能框架

> 一个完整的AI编程工作流框架，基于可组合的"技能"(skills)构建

## 核心理念

1. **先理解再编码** — 不急于写代码，先梳理需求和设计
2. **设计评审** — 将设计分块展示，逐步确认
3. **实施计划** — 分解为2-5分钟的小任务，每个任务有明确的文件路径、代码和验证步骤
4. **Subagent驱动开发** — 每个任务分配独立subagent执行，两阶段review（规格合规+代码质量）
5. **TDD强制执行** — RED-GREEN-REFACTOR循环，先写失败测试再写代码

## 核心技能

### 规划阶段
- **brainstorming** — 苏格拉底式需求梳理，探索替代方案
- **using-git-worktrees** — 创建隔离的git工作分支
- **writing-plans** — 生成详细的实施计划

### 开发阶段
- **subagent-driven-development** — Subagent逐任务执行+两阶段review
- **executing-plans** — 批量执行+人工检查点
- **test-driven-development** — 强制RED-GREEN-REFACTOR
- **dispatching-parallel-agents** — 并发subagent工作流

### 代码质量
- **requesting-code-review** — 按严重程度报告问题，关键问题阻断进度
- **receiving-code-review** — 响应审查反馈
- **systematic-debugging** — 4阶段根因分析

### 收尾阶段
- **finishing-a-development-branch** — 验证测试，merge/PR决策

## 支持平台

| 平台 | 安装方式 |
|------|---------|
| Claude Code | `/plugin marketplace add obra/superpowers-marketplace` → `/plugin install superpowers@superpowers-marketplace` |
| Cursor | `/add-plugin superpowers` |
| Codex | 手动安装 |
| OpenCode | 手动安装 |
| Gemini | `gemini extensions install` |

## 设计原则

- **Test-Driven Development** — 先写测试
- **Systematic over ad-hoc** — 系统化优于临时方案
- **Complexity reduction** — 简单性是首要目标
- **Evidence over claims** — 验证后再宣布成功

## 亮点

- Claude可自主工作2+小时不偏离计划
- 技能自动触发，无需手动干预
- 支持并发subagent加速开发

## 相关链接

- GitHub: https://github.com/obra/superpowers
- 博客: https://blog.fsck.com/2025/10/09/superpowers/
- Discord: https://discord.gg/Jd8Vphy9jq
- 许可证: MIT

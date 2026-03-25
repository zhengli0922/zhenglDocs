---
title: Claude Skill 编写的 9 个最佳实践
date: 2026-03-25
source: https://v.douyin.com/nA3aF-1YDt4/
author: 慢学AI
type: video
tags: [Claude, Skill, Agent, Claude-Code, 最佳实践]
---

# Claude Skill 编写的 9 个最佳实践

> 原文：Lessons from Building Claude Code: How We Use Skills（Claude Code 核心开发者 Styric）

## 核心框架：三层递进问题

| 层级 | 问题 | 目标 |
|------|------|------|
| 内容层 | Claude 能找到你的 skill 吗？能理解它该做什么吗？ | 被看见、被理解 |
| 结构层 | Skill 能在不同场景复用吗？会太僵化吗？ | 可复用、不僵化 |
| 高级技术层 | Skill 能记住上次做了什么吗？能生成可调用代码吗？ | 有状态、可组合 |

## 内容层（3条）

### 1. description 字段是给模型看的
- ❌ 错误：写成功能说明「这是一个监控 PR 的工具」
- ✅ 正确：写成触发条件「当用户说 babysit watch CI make sure this lands 时触发」
- description 决定**什么时候该用**，是 skill 被调用的第一道门槛

### 2. 不要陈述显而易见的事
- Claude 已经知道大量通用知识，skill 的价值在于**补充默认不知道的上下文、偏好和坑**
- 案例：Anthropic 的 frontend design skill 不教怎么写 React，只告诉 Claude「别再用 Inter 和紫色渐变了」

### 3. 构建 gotchas 部分
- Skill 里信号最强的内容是 **gotchas（踩坑记录）**，不是教程
- 随时间不断更新，把新踩的坑加进去

## 结构层（3条）

### 4. 使用文件系统和渐进式披露
- Skill 是文件夹不是文件：脚本、模板、数据文件分开存放
- 主文件只写核心逻辑，详细文档放 `references.md`，需要时让 Claude 自己去读

### 5. 仔细考虑设置流程
- 用 `config.json` 存储配置，首次运行时询问，后续直接使用
- 让 skill 从**无状态工具**变成**有状态助手**

### 6. 避免过度约束 Claude
- ❌ 错误：「先运行 test，再运行 lint，最后运行 build」（太死）
- ✅ 正确：「部署前确保代码通过测试、规范、构建」
- **约束目标，不约束路径**

## 高级技术层（3条）

### 7. 内存与数据存储
- Skill 每次运行都是全新的 → 让 skill 写日志，追加记录，下次只报告变化

### 8. 存储脚本并生成代码
- 把稳定能力**封成脚本和辅助函数**，让 Claude 负责组合，不是重造轮子
- 给 Claude 最好的工具是**可调用的代码**，不是更多文档

### 9. 按需 hooks
- 太严格的规则不想一直开启 → 用 hook 注册，只在当前会话有效
- 案例：careful skill 阻止危险命令（rm -rf、drop table）

## 核心观点

> 好的 skill 不是告诉 Claude 每一步做什么，而是给它**组合的能力**，让它在执行时自己决定怎么做。

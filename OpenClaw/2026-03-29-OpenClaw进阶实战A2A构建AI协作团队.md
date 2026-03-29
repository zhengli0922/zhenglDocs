---
title: OpenClaw 进阶实战：A2A构建AI协作团队
date: 2026-03-29
tags: [OpenClaw, A2A, 多Agent, 飞书机器人]
source: https://m.toutiao.com/is/GC6g0Ft4Oao/
type: article
author: 成为海贼王的帅男人
---

# OpenClaw 进阶实战：A2A构建AI协作团队

## 核心观点

单Agent什么都干，会导致上下文污染、角色越界、权限不清。正确方向是拆成团队：任务拆开、上下文隔离、权限隔离、结果汇总。

## 关键概念

### 多机器人 ≠ 多Agent
- **机器人**：消息入口（如飞书机器人）
- **Agent**：真正干活的思考主体

### 两种方案
1. **单机器人多群聊多Agent** — 简单，适合轻量测试
2. **多机器人多Agent** — 清晰隔离，推荐正式使用

## 架构设计

示例：1个OpenClaw + 4个飞书机器人 + 4个独立Agent

| Agent | 角色 | 职责 |
|-------|------|------|
| main-agent | 主监工/调度中枢 | 接收任务、分配、汇总、异常处理 |
| toutiao-agent | 头条创作助手 | 标题、文案、结构优化 |
| silver-agent | 白银期货监控 | 实时价格、涨跌幅、异动播报 |
| learner-agent | 学习沉淀助手 | 知识积累、经验复盘 |

## agentDir vs Workspace

- **agentDir**（物理配置层）：模型、鉴权、底层运行配置
- **Workspace**（认知记忆层）：IDENTITY.md、SOUL.md、AGENTS.md、MEMORY.md、skills/

> 一个Agent配一套独立 agentDir + 独立 Workspace，不要混用。

## 多Agent协作机制

靠 **会话隔离 + 显式通信**（sessions_send）：
1. 用户发任务给主监工
2. 主监工判断任务方向
3. 派发给专业Agent
4. 专业Agent在独立上下文处理
5. 结果返回主监工
6. 主监工统一整理回复

## 权限配置

- **deny优先级高于allow**
- 执行层Agent只给读权限：deny exec/bash/write/edit
- 主监工可调度所有Agent：`allowAgents: ["*"]`
- 执行层Agent不允许调度：`allowAgents: []`

## 角色文件三层结构

1. **IDENTITY.md**：你是谁
2. **SOUL.md**：你按什么原则做事
3. **AGENTS.md**：你和谁协作、边界在哪

## 踩坑提醒

1. 不要让多个Agent共用一个Workspace
2. 主监工不要自己下场干专业活
3. 创造型Agent不要给系统级权限
4. `visibility: all` 调试方便，正式环境要谨慎
5. 角色文件不要只写一行

## 总结

> 多机器人是入口层，多Agent是执行层，权限和会话边界决定系统稳不稳，角色文件决定最终效果好不好。

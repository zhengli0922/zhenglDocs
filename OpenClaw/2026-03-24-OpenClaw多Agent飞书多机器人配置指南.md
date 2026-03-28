---
title: OpenClaw多Agent+飞书多机器人配置完全指南
date: 2026-03-24
tags: [OpenClaw, 多Agent, 飞书, 机器人, 路由, Binding]
type: article
source: https://m.toutiao.com/is/T2HrqJwbqMs/
author: AI实战家
---

# OpenClaw多Agent+飞书多机器人配置完全指南

> 来源：今日头条 @AI实战家
> 收集时间：2026-03-24

## 核心观点

1. **Agent 是完全独立的 AI 实例**：拥有独立 Workspace、Agent Dir、Session Store、Model
2. **Binding 是路由规则**：决定消息发给哪个 Agent，流程为 `用户消息 → Gateway → 匹配 Binding → 路由到 Agent → AI 回复`
3. **三层架构**：飞书账号层（多个机器人）→ Binding 层（路由分发）→ Agent 层（独立 AI 大脑）

## 配置步骤

1. 让龙虾机器人创建 Agent
2. 创建飞书应用（每个 Agent 对应一个机器人）
3. 配置飞书 APP ID + Secret
4. 配置机器人权限、事件订阅（长连接）、发布应用
5. 创建群组，将机器人加入群组

## 路由规则优先级

| 优先级 | 匹配类型 | 说明 |
|--------|----------|------|
| 1 | peer 精确匹配 | 指定用户或群组 ID |
| 2 | accountId 匹配 | 指定飞书机器人账号 |
| 3 | channel 级别匹配 | 兜底路由 |

## 进阶技巧

- **不同 Agent 用不同模型**：产品用 Claude Sonnet、开发用 Opus、客服用 GLM-5
- **工具权限控制**：限制客服 Agent 只能查询，不能执行敏感操作
- **群组精准路由**：通过 peer 匹配实现一个机器人入口多个后端 Agent

## 关键要点

- 每个 Agent 会话完全隔离，不会串台
- 共享技能放 `~/.openclaw/skills/`，专属技能放各 Agent 的 `skills/`
- Gateway 重启不影响会话，会话存储在 `~/.openclaw/agents/<agentId>/sessions/`

## 参考文档

- 官方文档：https://docs.openclaw.ai
- 多 Agent 路由：https://docs.openclaw.ai/concepts/multi-agent
- 飞书机器人：https://docs.openclaw.ai/channels/feishu

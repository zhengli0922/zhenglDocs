---
title: OpenClaw多Agent工作流配置教程
date: 2026-03-27
tags: [OpenClaw, multi-agent, 飞书, 教程]
source: https://v.douyin.com/DXioJiiKPHY/
type: video
author: 海瑞hary
---

# OpenClaw多Agent工作流配置教程

## 核心问题

OpenClaw 对话是单线程的，一个指令没做完前无法下发新任务。多 Agent 可以并行处理不同任务。

## 使用场景

- 一个 Agent 处理视频时，另一个可以处理文件
- 不同 Agent 承担不同角色（编程助手、私人助理等）

## 配置步骤

### 1. 创建新 Agent
- 在 OpenClaw 界面添加 Agent，定义名字和工作区

### 2. 对接飞书
- 飞书开放平台 → 创建企业自建应用（为每个 Agent 准备一个机器人）
- OpenClaw 界面 → 飞书频道 → 添加新配置，填入 App ID 和 App Secret
- 新建渠道，订阅方式选长链接，添加事件
- 用配对码授权

### 3. 对话测试
- 授权完成后即可通过飞书与新 Agent 对话

## 角色示例

| Agent | 职责 |
|-------|------|
| 巴巴塔 | 编程、严谨任务 |
| 银月 | 私人助理、情绪价值 |
| 穆佩宁 | 新建示例 |

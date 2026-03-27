---
title: "Claude Code 刚刚发布了 Memory 2.0"
date: 2026-03-27
tags: [Claude-Code, memory, AutoDream, AI记忆, 自动化]
source: https://m.toutiao.com/is/xpeoeYaNOJ4/
type: article-note
author: 数码科技早知道
---

# Claude Code 刚刚发布了 Memory 2.0

> 作者：数码科技早知道
> 来源：今日头条
> 日期：2026-03-26

## 核心事件

Anthropic 为 Claude Code 发布了实验功能 **AutoDream（自动做梦）**——后台自动整理长期记忆的机制。

## AutoDream 是什么

- 不是"多记一点"，而是给你一个后台的"整理员"
- 周期性拉起子 agent，回看多轮会话
- 对记忆文件进行**合并、压缩、修剪、刷新**
- 状态栏会显示 `dreaming`

> 类比：AutoMemory = 边走边捡东西塞进背包；AutoDream = 回家后把背包倒出来按类别归档

## 使用方式

- `/memory` — 进入记忆管理界面，查看 AutoDream 开关
- `/dream` — 手动触发一次"做梦"
- 目前是逐步推送的实验功能，不是所有人都有

## AutoDream 做的四件事

1. **Merge** — 合并相似记忆
2. **Prune** — 删除不必要的内容
3. **Refresh** — 更新过时信息
4. **Compact** — 压缩冗余内容

## 关键洞察

### 记忆应该是索引，不是倾倒
理想的 memory.md 不该变成"聊天记录第二份"，而应该变成"目录 + 要点 + 链接"。

### 上下文越多 ≠ 越好
更长只会带来：成本上升、注意力被稀释。AutoDream 逼 AI 记得更精，不是更多。

### 召回优化
球池里 100 个球，99 个蓝球 1 个粉球。找粉球最聪明的做法不是倒进更多球，而是先拿走一半蓝球。

## 触发机制（推测）

- 按时间触发：如每 12 小时做一次 dream
- 按会话数触发：如累计 300 会话做一次 dream
- 只改记忆文件（md），不动代码

## 注意点

- 记忆是全局开启的，但 AutoDream 按项目分别整理
- 前台提示可能混乱（"unknown skill"），但后台已开工
- 项目越大，复盘会话越多（演示中有 285 个会话）

## 我的思考

这个机制和 OpenClaw 的 session compaction + memory flush 思路一致，但 AutoDream 更自动化、更深层。对于冰淇淋来说，目前 MEMORY.md + 手动压缩够用，但这个方向值得关注——未来 OpenClaw 可能也会内置类似机制。

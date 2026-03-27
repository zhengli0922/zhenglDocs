---
title: OpenClaw + Obsidian 联动：打造个人知识管理神器
date: 2026-03-23
tags: [OpenClaw, Obsidian, 知识管理, 自动化, 工作流]
source: https://www.toutiao.com/article/7620298373296128547/
type: article
author: 养虾人
platform: 今日头条
---

# OpenClaw + Obsidian 联动：打造个人知识管理神器

让AI助手帮你自动整理笔记、生成知识图谱

## 为什么需要这个组合？

Obsidian 是当下最火的本地知识管理工具，而 OpenClaw 是你的AI助手。两者结合，可以实现：

- **自动整理笔记** - AI帮你分类、打标签、提取重点
- **智能知识问答** - 直接问AI你的笔记内容
- **自动生成文章** - 基于笔记素材快速产出内容
- **知识图谱构建** - AI帮你发现笔记间的关联

## 准备工作

1. 安装 Obsidian：https://obsidian.md
2. 安装 OpenClaw（参考之前的安装教程）
3. 安装必要技能：`file-manager`、`obsidian-tools`

## 配置步骤

### 第一步：连接 Obsidian 仓库

```yaml
# ~/.config/openclaw/config.yaml
knowledge_base:
  obsidian_path: "D:/Obsidian Vault"
```

### 第二步：创建自动化工作流

```yaml
name: Obsidian 笔记整理
steps:
  - name: 读取新笔记
    action: file.read
    input: "{{vault_path}}/Inbox/*.md"
  - name: AI分析内容
    action: llm.analyze
    prompt: |
      分析以下笔记内容，提取关键信息：
      1. 主题分类
      2. 重要标签
      3. 核心观点摘要
      4. 建议的存放位置
      内容：{{content}}
  - name: 移动整理
    action: file.move
    source: "{{file_path}}"
    target: "{{vault_path}}/{{category}}/{{new_filename}}"
```

### 第三步：设置自动触发

```bash
# 每小时检查一次 Inbox
openclaw schedule add --workflow obsidian_workflow --cron "0 * * * *"
```

## 实战场景

### 场景1：网页剪藏自动整理
浏览器插件剪藏 → Obsidian Inbox → OpenClaw 自动分析 → AI提取关键信息 → 自动归档

### 场景2：会议记录智能处理
语音转文字 → 存入 Obsidian → OpenClaw 自动提取待办事项、关键决策、行动项 → 生成结构化会议纪要

### 场景3：知识问答
直接在 OpenClaw 中提问，AI 从笔记库中检索相关内容

## 高级技巧

1. **双向链接自动发现** - 让 AI 发现笔记间的潜在关联
2. **每日知识回顾** - 定时任务推送复习卡片
3. **写作素材库** - 基于笔记自动生成写作素材

## 效果对比

| 指标 | 使用前 | 使用后 |
|------|--------|--------|
| 笔记整理时间 | 30分钟/天 | 5分钟/天 |
| 知识查找时间 | 5分钟/次 | 10秒/次 |
| 内容产出效率 | 1篇/周 | 3篇/周 |

## 备注

> 文章中的配置示例（如 `obsidian_path`、工作流YAML、`openclaw schedule`）为概念性描述，实际 OpenClaw 配置方式可能不同，仅供参考思路。

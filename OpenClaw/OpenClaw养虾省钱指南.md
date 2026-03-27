---
title: OpenClaw养虾省钱指南
date: 2026-03-23
tags: [OpenClaw, AI工具]
source: https://developer.aliyun.com/article/1717434
type: knowledge
---
# OpenClaw 养虾省钱指南 - 烧1亿Token总结

> 来源：今日头条 - 阿里云开发者社区
> 链接：https://developer.aliyun.com/article/1717434
> 整理时间：2026-03-22
> 标签：#OpenClaw #省钱 #Token优化 #配置

---

## 🔥 核心真相：Token 都被谁吃了？

### Token 消耗占比

| 来源 | 占比 |
|------|------|
| 历史对话上下文 | 30%~40% |
| 工具调用返回内容 | 20%~30% |
| 工具 Schema 结构注入 | 10%~15% |
| Thinking 思考模式输出 | 10%~50% |

**你输入的那几句话，连冰山一角都算不上！**

---

## ✅ 新手必开 6 大设置

### 1. 实时日志跟踪
```bash
openclaw logs --follow
```
**作用**：实时看 AI 思考、调用工具、消耗情况

### 2. 开启流式回复
```bash
openclaw config set channels.default.streaming true
```
**作用**：边出字边看，错了立刻停

### 3. 开启耗时显示
```bash
openclaw config set channels.default.footer.elapsed true
```

### 4. 开启状态显示
```bash
openclaw config set channels.default.footer.status true
```

### 5. 群聊@才回复
```bash
openclaw config set channels.default.requireMention true
```
**作用**：防止疯狂烧钱

### 6. 话题独立上下文
```bash
openclaw config set channels.default.threadSession true
```
**作用**：多任务不串、不爆 Token

---

## 🚨 4 条保命指令

| 指令 | 作用 |
|------|------|
| `/stop` | 立即停止任务，止损 Token |
| `/status` | 查看状态、Token 消耗 |
| `/compact` | **最强省钱** - 压缩上下文，省 30%~40% |
| `/new` | 新开对话，清空历史 |

---

## ⚙️ 进阶省钱配置

### 上下文自动压缩
```bash
openclaw config set agents.defaults.compaction.mode default
openclaw config set agents.defaults.compaction.enabled true
```

### 自动清理过期上下文
```bash
openclaw config set agents.defaults.contextPruning.mode cache-ttl
openclaw config set agents.defaults.contextPruning.ttl 4h
```

### 限制最大上下文长度
```bash
openclaw config set agents.defaults.maxContextTokens 4096
```

### 限制最大执行步骤
```bash
openclaw config set agents.defaults.maxSteps 15
```

### 关闭冗余 Thinking 输出
```bash
openclaw config set model.parameters.thinking false
```

### 生效命令
```bash
openclaw gateway restart
```

---

## 💰 阿里云百炼 Coding Plan

### 免费额度
- **7000 万 Token**
- **90 天有效期**

### API Key 特征
- 以 `sk-sp-` 开头

### 配置示例
```json
{
  "model": {
    "provider": "alibaba-cloud",
    "apiKey": "你的百炼API-Key",
    "baseUrl": "https://dashscope.aliyuncs.com/compatible-mode/v1",
    "defaultModel": "bailian/qwen-turbo",
    "parameters": {
      "temperature": 0.3,
      "maxTokens": 2048,
      "stream": true,
      "thinking": false
    }
  },
  "agent": {
    "compaction": {
      "mode": "default",
      "enabled": true
    },
    "contextPruning": {
      "mode": "cache-ttl",
      "ttl": "4h"
    },
    "maxContextTokens": 4096,
    "maxSteps": 15
  }
}
```

---

## 📋 日常省钱习惯

- ✅ 每 10~15 轮对话：发 `/compact`
- ✅ 切换任务：发 `/new`
- ✅ 简单问题：用轻量模型
- ✅ 复杂任务：再切强模型
- ✅ 经常用 `/status` 看消耗
- ✅ 群聊一定开 `requireMention true`

---

## 🔧 常见问题

### Token 消耗还是很快
- 没开上下文压缩
- 没发 `/compact`
- 历史对话太长
- 开启了 Thinking 模式

### 群聊疯狂回复、烧 Token
- 没开 `requireMention true`
- 没开 `threadSession`

### 修改配置不生效
- 忘记执行 `openclaw gateway restart`

---

## 📊 效果对比

| 配置前 | 配置后 |
|--------|--------|
| 100% Token | 20%~30% Token |

---

## 🎯 总结

**养虾先省钱，6+4+优化是核心**

- 6 个必开设置
- 4 个神指令
- 2 套进阶优化
- 全套省钱配置：消耗压到原来 30% 以内

---

*整理：冰淇淋🍦*

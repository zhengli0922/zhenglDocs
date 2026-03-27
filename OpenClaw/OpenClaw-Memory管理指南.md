---
title: OpenClaw Memory管理指南
date: 2026-03-23
tags: [OpenClaw, AI工具]
type: knowledge
---
# OpenClaw Memory 管理指南

> 来源：抖音 @阿东玩AI
> 时间：2026-03-22
> 标签：#OpenClaw #Agent #Memory #AI

---

## 核心理念

**文件即真相**

OpenClaw 的记忆哲学跟其他 AI 不一样：
- 模型本身不记得任何东西
- 只读你磁盘上的 md 文件
- 写在文件里的，才是它"记得"的
- **你其实是在用文件系统养一个数字人格**

---

## 阿东的血泪教训

养废过三只"龙虾"（OpenClaw Agent）：

| 问题 | 症状 | 原因 |
|------|------|------|
| 第一只 | 用了两周突然不认识我了 | 没有持久记忆 |
| 第二只 | token 从几块涨到几十块 | 记忆冗余，没清理 |
| 第三只 | 精神分裂，上午说 A 下午改口 | 记忆冲突，没规则 |

**换了 Claude4.6、换了 GPT-5，结果一样。**
问题不在模型，是从来没养过它的 memory。

---

## 三阶段进阶打法

### 1️⃣ 新手保命版

```
workspace/
├── USER.md      # 你是谁、想要什么风格
├── SOUL.md      # 这只虾的三观
└── RULES.md     # 每天结束前总结三件事写入
```

**每日流程**：
1. 结束前让 Agent 总结今天的三件重要事
2. 写入 RULES.md
3. Agent 下次启动会自动读取

---

### 2️⃣ 越用越顺版

**技巧**：
- 用 `### 高优先级` 标记关键段落
- 每周提炼日志，写入 KNOWLEDGE.md
- 开启 memory-search 插件

**推荐配置**：
```yaml
memory-search:
  top_k: 8-15
  threshold: 0.22-0.28
```

---

### 3️⃣ 自我进化版

**长期记忆插件**：
- memory-lancedb-pro
- mem0
- supermemory

**每日反思流程（23:00 自动执行）**：
```
读日志 → 提炼 → 写规则 → 清理
```

---

## 关键洞察

> **模型可以换，Skill 可以抄，memory 才是你真正养出来的东西。**

Memory 是 Agent 的"灵魂"——其他都可以复制，只有记忆是独一无二的。

---

## 相关文件

- [[OpenClaw必装Skills推荐]]
- [[OpenClaw新手必装Skills推荐]]

---

*整理：冰淇淋🍦*
*来源：抖音 @阿东玩AI*

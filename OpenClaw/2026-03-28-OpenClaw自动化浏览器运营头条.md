---
title: OpenClaw 自动化操作浏览器运营头条
date: 2026-03-28
tags: [openclaw, 浏览器自动化, 头条运营, AI自媒体, CDP, 自动发布]
source: https://m.toutiao.com/is/L_h25JmOmKc/
type: video-note
author: AI陪我搞钱（张麻子/Claude AI）
---

# OpenClaw 自动化操作浏览器运营头条

> 博主：AI陪我搞钱 | 发布：2026-03-28 | 运营3天实战经验

## 系统架构

3个 skill + 主流程配置：
- **toutiao-operations**：头条运营主 skill（账号信息、工作节奏、写作规范、发布流程、Chrome DevTools 连接）
- **article-writing**：文章写作 skill（AI第一人称、费曼学习法行文逻辑）
- **intel-report**：AI情报日报 skill（定时用 Exa API 搜 AI 圈情报）
- **模型配置**：日常 claude-sonnet-4-6（快），文章 claude-opus-4-6（质量）

## 自动发布流程（cron：早8/午12/晚6）

1. **读飞书日志** — 每次新会话，先从飞书日志拿回上下文
2. **查数据+写内容** — 调头条内部 API 查数据 + Exa 搜情报 → 组合微头条
3. **browser tool 发布** — snapshot → click → type → click 发布（走 CDP 端口 18800）
4. **更新飞书日志** — append 发布记录，下次任务能读到

## 头条内部 API（CDP 直接调）

| 接口 | 用途 |
|------|------|
| `/mp/agw/creator_center/user_info` | 粉丝数 |
| `/mp/agw/creator_center/list/v2` | 每篇展现/阅读/点击率 |
| `/mp/agw/comment/list` | 待回复评论 |

## 长文章发布

- 正文填充：`document.execCommand('insertText')` 往 ProseMirror 编辑器塞文字，1200+字分块
- 配图：HTML → browser 截图 → 上传飞书 → 插入文档
- ⚠️ **翻车点**：头条 `monitor_browser` 模块检测 `[Risk] Mouse` 特征（事件间隔太均匀），拦截自动化发布操作。长文章「确认发布」需人工点

## 评论批量回复

DOM 结构 `.all-comment-item-wrap`，逐条：定位 → 点评论图标 → 填内容 → 发布。3天回复7条，全程无人。

## 记忆管理（三层机制）

1. **飞书日志** = 跨会话持久化（最重要，忘更新 = 当天白干）
2. **本地 memory 文件** = 主会话用（`memory/日期.md` + `MEMORY.md`）
3. **skill 文件** = 结构化操作记忆（踩坑记录、连接方式、已知限制）

## 技术坑

| 坑 | 原因 | 解决方案 |
|----|------|---------|
| Chrome 146+ | default profile + 调试端口不兼容 | 用 OpenClaw 独立 profile |
| React 合成事件 | 原生 click() 不触发 | 找 `__reactEventHandlers$xxx.onClick` |
| Garfish 微前端 | DOM 在容器内，querySelector 找不到 | 先定位容器再往里找 |
| [Risk] Mouse | 头条反自动化检测 | ❌ 无完全绕过方案 |

## 3天数据

- 粉丝：406 → 408（+2）
- 最高单篇：展现 8985，阅读 1621，点击率 18%
- 定时任务稳定运行：早/午/晚三条微头条自动发布
- 文章发布：内容全自动，最后发布靠人工

## 关键结论

> 自动化能解决 90% 的重复劳动，剩下 10% 是平台的防守机制。

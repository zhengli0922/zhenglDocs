---
title: Browser Use CLI 2.0 来了：让AI像人一样操作浏览器
date: 2026-03-26
tags:
  - Browser-Use
  - Playwright
  - 浏览器自动化
  - AI工具
source: https://m.toutiao.com/is/OdM2zKfZQ1s/
type: article
author: 职场AI效率指南
---

# Browser Use CLI 2.0 来了：让AI像人一样操作浏览器

> 来源：今日头条 · 职场AI效率指南 · 2026-03-26

## 两条路，底层逻辑不一样

| | Playwright MCP | Browser Use CLI 2.0 |
|--|--|--|
| 思路 | 精确操控 | 语义理解 |
| 用法 | 写代码告诉AI每一步 | 说人话"帮我登录Gmail" |
| Token消耗 | ~114k/次 | ~27k/次（**4倍差距**） |
| 速度 | 3-5秒/次 | ~50毫秒/次（常驻daemon） |
| 登录态 | 需要重新验证 | **可连接已登录的Chrome** |

## 怎么选

**选 Playwright MCP：**
- 操作流程固定，每天重复
- 需要精确控制每一步
- 愿意花时间写代码

**选 Browser Use CLI 2.0：**
- 任务多变开放，如"帮我填这张表"
- 不想研究网页结构
- 需要保留登录状态
- 想快速搞定，不想写代码

## Browser Use CLI 安装

```bash
curl -fsSL https://browser-use.com/cli/install.sh | bash
browser-use doctor
```

## 连接真实Chrome

```bash
# 启动带调试端口的Chrome
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --remote-debugging-port=9222

# 连接
browser-use connect chrome
```

## 结论

- 固定流程 → Playwright
- 开放任务 → Browser Use
- Browser Use 的保留登录态是杀手级功能
- 任务量不大的话，两者实际花费差异可忽略

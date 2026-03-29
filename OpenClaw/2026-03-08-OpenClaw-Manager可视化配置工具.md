---
title: OpenClaw的可视化配置工具—OpenClaw Manager
date: 2026-03-08
tags: [OpenClaw, openclaw-manager, 可视化配置, Tauri, GUI]
source: https://m.toutiao.com/is/argRAjjw498/
type: article
author: zpmedx
---

# OpenClaw的可视化配置工具—OpenClaw Manager

高性能跨平台 AI 助手管理工具，基于 Tauri 2.0 + React + TypeScript + Rust 构建。

- GitHub: https://github.com/miaoxworld/openclaw-manager
- Releases: https://github.com/miaoxworld/openclaw-manager/releases

## 快速使用

直接从 Releases 页面下载对应版本安装，点击绿色三角箭头可直接启动 OpenClaw。

## 自行构建

### 环境要求

- Node.js >= 18.0
- Rust >= 1.70
- pnpm（推荐）或 npm
- Microsoft C++ Build Tools
- WebView2

### 构建步骤

1. **安装 Rust**：https://rust-lang.org/zh-CN/tools/install/ ，管理员运行安装程序，选择1回车
2. **安装 WebView2**：设置→应用→安装的应用查看是否已有 Microsoft Edge WebView2 Runtime，没有则从 https://developer.microsoft.com/zh-cn/microsoft-edge/webview2 下载
3. **构建**：
   ```powershell
   npm install
   npm run tauri:build
   ```
   - 构建可能报 msi 格式转换 Error，但 .exe 已生成，在 `src-tauri/target/release/bundle/` 目录可直接运行

## 注意

- 建议构建前设置系统还原点
- 作者测试环境：Windows 11，i7-13620H，16G+1T

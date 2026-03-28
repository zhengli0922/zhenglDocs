---
title: ComfyUI Skills - 为小龙虾打造专属图像生成工具
date: 2026-03-28
tags: [comfyui, openclaw, AI绘图, workflow, agent]
source: https://m.toutiao.com/is/aJIiSUzmwVg/
type: video-note
author: 于火炉通行
---

# ComfyUI Skills - 为小龙虾打造专属图像生成工具

> 博主：于火炉通行 | 发布：2026-03-25

## 核心思路

将 ComfyUI（Diffusion 开源编排工具）与 OpenClaw/小龙虾打通，让 AI Agent 能理解、调用、甚至自动优化你的 ComfyUI 工作流。

- ComfyUI GitHub 85k+ star，社区认可度高
- 很多工业级应用场景都在用 ComfyUI
- 目的：**盘活已有的 workflow 资产**，通过手机（飞书/Discord/QQ）远程调用

## 安装部署

1. 在 GitHub 找到中文安装文档
2. 克隆项目到本地
3. 创建虚拟环境，安装依赖
4. 复制配置文件
5. 执行启动脚本（macOS/Linux）

## 配置工作流

在前端管理面板中：

1. **选择服务器** — 默认本地（localhost + 端口），支持配置多个远端服务器
2. **导入工作流** — 自动读取工作流节点
3. **参数暴露** — 选择哪些参数让 AI 调整，哪些作为常量固定
4. **添加描述** — 写清楚工作流用途，让 Agent 理解
5. **保存配置**

## 使用方式

配置完成后，在飞书中直接对话小龙虾：
- 让它识别已配置的工作流
- 描述需求，Agent 自动选择合适的 workflow 调用
- 遇到报错可自动优化参数（如 VAE/checkpoint 选错会自动查找替换）

## 进阶功能

- **多服务器管理** — 本地 + 远端，支持添加多个 ComfyUI 实例
- **配置导入/导出** — 一键迁移所有工作流配置到新机器
- **版本更新** — 工作流更新后可上传新版本，不覆盖已有的参数注释
- **参数映射优化** — 手动修改 AI 对参数的理解描述

## 关键价值

- workflow 积累多了，Agent 能帮你记住所有工作流的功能和适用场景
- 多个 workflow 组合使用，解决复杂任务
- 没思路时问 Agent，它可能从你的资产中找到解决方案

## 注意事项

- 公网部署 ComfyUI 必须做访问控制，否则服务器会被滥用
- 支持 OpenClaw、Claude Code、Cursor、Google Agent、OpenAI Codex 等支持 Skills 的 Agent

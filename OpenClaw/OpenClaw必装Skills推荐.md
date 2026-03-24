# OpenClaw 必装 Skills 推荐

> 来源：今日头条 - "别再装一堆没用的Skills了!OpenClaw新手第一批..."
> 整理时间：2026-03-22
> 标签：#OpenClaw #Skills #效率工具

---

## ⚠️ 核心警告

**ClawHub 上 80% 的技能是垃圾或恶意的！**

安装前必须：
1. 访问 ClawHub 网站验证
2. 检查 **Security Scan = Benign**
3. 不要直接安装，先验证安全性

---

## 🏆 Top 10 推荐 Skills

### 1. Composio ⭐⭐⭐ 最推荐

**用途**：一个集成解锁 860+ 外部工具（GitHub、Slack、Gmail 等）

**安装**：
```bash
cd ~/.openclaw/skills
npx skills add composioq/skills
# 选择 OpenClaw，其余默认
```

**场景**：
- 构建 AI Agent 访问 Gmail、Slack
- 多租户 SaaS 应用
- 事件驱动自动化

---

### 2. Reverse Engineering

**用途**：逆向工程网络协议，分析流量

**安装**：https://skills.sh/wshobson/agents/protocol-reverse-engineering

**场景**：
- 捕获分析网络流量
- 开发 Wireshark 解析器
- TLS 指纹分析

---

### 3. Frontend Design

**用途**：产出高质量 UI，避免千篇一律的紫色渐变

**安装**：https://skills.sh/anthropics/skills/frontend-design

**场景**：
- 快速原型设计
- 独特风格落地页
- 打破模板化设计

---

### 4. Self-Improving Agent

**用途**：让 OpenClaw 记住错误和偏好，越用越聪明

**安装**：https://clawhub.ai/pskoett/self-improving-agent

**场景**：
- 记录错误避免重复
- 存储用户偏好
- 持续改进

---

### 5. Eleven Labs Agent

**用途**：给 OpenClaw 真实声音，支持电话呼叫

**安装**：https://clawhub.ai/PennyroyalTea/elevenlabs-agents
**要求**：ElevenLabs API Key

**场景**：
- 邮件/短信失败后自动打电话
- 语音任务自动化
- 语音摘要

---

### 6. N8N Workflow

**用途**：用对话控制 N8N 自动化工作流

**安装**：https://clawhub.ai/KOwl64/n8n-workflow-automation

**场景**：
- 触发复杂工作流
- 无需订阅的自动化
- 本地隐私保护

---

### 7. Exa Search

**用途**：开发者专用搜索引擎，避免 SEO 垃圾

**安装**：https://clawhub.ai/fardeenxyz/exa
**要求**：EXA_API_KEY

**场景**：
- 查找最新技术文档
- 搜索代码示例
- 减少幻觉

---

### 8. Vercel

**用途**：自然语言部署管理 Vercel 项目

**安装**：https://clawhub.ai/TheSethRose/vercel

**场景**：
- 部署网站
- 触发构建
- 查看日志

---

### 9. OpenAI Whisper

**用途**：本地运行语音转文字

**安装**：https://clawhub.ai/steipete/openai-whisper
**要求**：OpenAI API Key

**场景**：
- 离线转录音频
- 会议记录转文字
- 生成字幕

---

### 10. Home Assistant

**用途**：自然语言控制智能家居

**安装**：https://clawhub.ai/iAhmadZain/home-assistant

**场景**：
- 控制智能设备
- 创建自动化场景
- 本地隐私保护

---

## 📦 其他有用的 Skills

| Skill | 用途 |
|-------|------|
| Model Usage | 监控 API Token 使用量 |
| WhatsApp CLI | 自然语言发送 WhatsApp |
| Bird (Twitter/X) | 搜索 Twitter 数据 |
| YouTube Summarizer | 总结 YouTube 视频 |
| GA4 Analysis | Google Analytics 分析 |
| GNO | 本地文档搜索索引 |

---

## 🔧 安装方法

### 方法1：Skills.sh（推荐）

```bash
# 1. 访问 https://skills.sh 找到技能
# 2. 安装：
cd ~/.openclaw
npx skills add <技能URL>
# 3. 选择 OpenClaw，按空格选择，回车确认
```

### 方法2：ClawHub

```bash
# 1. 访问 https://clawhub.ai
# 2. 搜索技能
# 3. 检查 Security Scan = Benign
# 4. 复制安装命令：
npx clawhub@latest install <技能名>
```

---

## 💡 最佳实践

1. **不要装太多** - 只安装真正需要的
2. **先验证安全** - 必须检查 Security Scan
3. **定期清理** - 删除不用的技能
4. **推荐 Composio** - 一个替代 860+ 单独集成

---

## 📊 我的技能管理

**已安装（保留）**：
- ✅ tavily-search - 网络搜索
- ✅ cn-web-search - 中文搜索
- ✅ xiaohongshu-mcp-skill - 小红书
- ✅ chrome-devtools-mcp - 浏览器自动化
- ✅ snowflake-mcp - 数据库
- ✅ skill-manager - 技能管理

**已删除**：
- ❌ sonoscli - 无 Sonos 设备
- ❌ baidu-search - 已有 tavily

**待安装**：
- ⏳ Composio - 860+ 工具集成
- ⏳ Frontend Design - UI 设计
- ⏳ Self-Improving Agent - 自我改进

---

## 📌 关键要点

1. **ClawHub 80% 是垃圾** - 安装前必须验证
2. **推荐 Composio** - 一个顶 860+ 个
3. **安全第一** - 检查 Security Scan
4. **按需安装** - 不要装一堆没用的

---

*整理：冰淇淋🍦*

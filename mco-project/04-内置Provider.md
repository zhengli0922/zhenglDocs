# MCO 内置 Provider

> 本文档详细说明 MCO 支持的 AI Agent Provider

---

## 内置 Provider 列表

| Provider | CLI 命令 | 状态 |
|----------|----------|------|
| Claude Code | `claude` | ✓ 已支持 |
| Codex CLI | `codex` | ✓ 已支持 |
| Gemini CLI | `gemini` | ✓ 已支持 |
| OpenCode | `opencode` | ✓ 已支持 |
| Qwen Code | `qwen` | ✓ 已支持 |

---

## 1. Claude Code

### 基本信息

| 项目 | 说明 |
|------|------|
| CLI 命令 | `claude` |
| 开发商 | Anthropic |
| 模型 | Claude 4.5/4.6 系列 |

### 默认权限配置

```json
{
  "permission_mode": "plan"
}
```

### 使用示例

```bash
mco review \
  --repo . \
  --prompt "Review for security issues." \
  --providers claude
```

### 特点

- 强大的推理能力
- 优秀的代码理解能力
- 支持长上下文

---

## 2. Codex CLI

### 基本信息

| 项目 | 说明 |
|------|------|
| CLI 命令 | `codex` |
| 开发商 | OpenAI |
| 模型 | GPT-4 / GPT-4o 系列 |

### 默认权限配置

```json
{
  "sandbox": "workspace-write"
}
```

### 使用示例

```bash
mco review \
  --repo . \
  --prompt "Review for bugs." \
  --providers codex
```

### 特点

- 代码生成能力强
- 与 GitHub 生态集成
- 支持 PR 审查

---

## 3. Gemini CLI

### 基本信息

| 项目 | 说明 |
|------|------|
| CLI 命令 | `gemini` |
| 开发商 | Google |
| 模型 | Gemini 2.x 系列 |

### 使用示例

```bash
mco review \
  --repo . \
  --prompt "Review for performance issues." \
  --providers gemini
```

### 特点

- 多模态能力
- 长上下文支持
- 与 Google Cloud 集成

---

## 4. OpenCode

### 基本信息

| 项目 | 说明 |
|------|------|
| CLI 命令 | `opencode` |
| 类型 | 开源 CLI 工具 |
| 模型 | 支持多种后端 |

### 使用示例

```bash
mco review \
  --repo . \
  --prompt "Review code quality." \
  --providers opencode
```

### 特点

- 开源免费
- 支持多种模型后端
- 可自定义配置

---

## 5. Qwen Code

### 基本信息

| 项目 | 说明 |
|------|------|
| CLI 命令 | `qwen` |
| 开发商 | 阿里云 |
| 模型 | Qwen 2.5 Coder 系列 |

### 使用示例

```bash
mco review \
  --repo . \
  --prompt "审查代码安全问题。" \
  --providers qwen
```

### 特点

- 中文支持优秀
- 代码能力强
- 开源可用

---

## Provider 权限配置

### 默认权限

| Provider | 权限 Key | 默认值 |
|----------|----------|--------|
| `claude` | `permission_mode` | `plan` |
| `codex` | `sandbox` | `workspace-write` |

### 自定义权限

使用 `--provider-permissions-json` 参数：

```bash
mco review \
  --repo . \
  --prompt "Review code" \
  --providers claude,codex \
  --provider-permissions-json '{"claude": {"permission_mode": "acceptEdits"}}'
```

---

## Provider 超时配置

### 全局超时

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--stall-timeout` | 900 | 无输出进展超时（秒） |
| `--review-hard-timeout` | 1800 | 硬截止时间（秒） |

### 单个 Provider 超时

使用 `--provider-timeouts` 参数：

```bash
mco review \
  --repo . \
  --prompt "Review code" \
  --providers claude,codex,qwen \
  --provider-timeouts qwen=900,codex=900
```

---

## 多 Provider 组合使用

### 全量审查

```bash
mco review \
  --repo . \
  --prompt "全面审查代码质量、安全性和性能。" \
  --providers claude,codex,gemini,opencode,qwen
```

### 安全审查组合

```bash
mco review \
  --repo . \
  --prompt "安全漏洞审查" \
  --providers claude,codex,gemini \
  --format sarif
```

### 性能审查组合

```bash
mco review \
  --repo . \
  --prompt "性能问题审查" \
  --providers gemini,qwen
```

### 架构分析组合

```bash
mco run \
  --repo . \
  --prompt "分析项目架构，识别设计问题和改进机会。" \
  --providers claude,gemini,qwen
```

---

## 适配器契约

每个 Provider 通过统一的适配器契约运行：

```
┌────────────────────────────────────────────────────────┐
│                    Adapter Contract                     │
├────────────────────────────────────────────────────────┤
│  1. Detect  — 检测二进制文件和认证状态                    │
│  2. Run     — 启动 CLI 进程，传入提示词                   │
│  3. Poll    — 监控进程状态 + 输出字节增长                 │
│  4. Cancel  — 超时时发送 SIGTERM/SIGKILL                │
│  5. Normalize — 从原始输出中提取结构化 findings          │
└────────────────────────────────────────────────────────┘
```

### 扩展新 Provider

添加新的 Agent CLI 只需实现三个钩子：

1. **认证检查** — 检查 CLI 是否可用、是否已认证
2. **命令构建** — 构建执行命令和参数
3. **输出标准化** — 解析输出，提取结构化 findings

---

## 选择建议

### 按任务类型选择

| 任务类型 | 推荐 Provider |
|----------|---------------|
| 安全审查 | claude, codex, gemini |
| 性能分析 | gemini, qwen |
| 架构评估 | claude, gemini |
| 代码质量 | 全部 |
| 中文项目 | qwen + claude |

### 按预算选择

| 预算级别 | 推荐 Provider |
|----------|---------------|
| 高 | 全部 5 个并行 |
| 中 | claude, codex, qwen |
| 低 | opencode + qwen |

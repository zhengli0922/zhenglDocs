# MCO CLI API 文档

> 本文档详细说明 MCO 的命令行接口

---

## 命令概览

```
mco
├── review      # 结构化代码审查
├── run         # 通用任务执行
├── doctor      # 环境健康检查
└── agent       # Agent 注册表管理
    ├── list    # 列出所有 Agent
    └── check   # 检查单个 Agent
```

---

## 通用参数

### 基本参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--repo` | `.` | 仓库路径 |
| `--prompt` | - | 任务提示词 |
| `--providers` | `claude,codex` | Provider 列表（逗号分隔） |
| `--json` | 关闭 | JSON 格式输出 |

### 路径约束参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--allow-paths` | - | 允许访问的路径列表 |
| `--target-paths` | - | 目标审查路径 |
| `--enforcement-mode` | `strict` | 执行模式：`strict` 或 `permissive` |

### 超时参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--stall-timeout` | `900` | 无输出进展超时（秒） |
| `--review-hard-timeout` | `1800` | 硬截止时间（秒），`0` 禁用 |
| `--provider-timeouts` | - | 单个 Provider 超时覆盖 |

### 并行度参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--max-provider-parallelism` | `0` | 最大并行度，`0` = 全并行 |

---

## mco review

### 功能

结构化代码审查，输出标准化的 findings。

### 语法

```bash
mco review --repo <path> --prompt "<prompt>" [options]
```

### 基本示例

```bash
mco review \
  --repo . \
  --prompt "Review for security vulnerabilities and performance issues." \
  --providers claude,codex,gemini \
  --json
```

### Review 专用参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--format` | `report` | 输出格式：`report`, `markdown-pr`, `sarif` |
| `--strict-contract` | 关闭 | 强制 findings JSON 契约 |
| `--synthesize` | 关闭 | 执行共识总结 |
| `--synth-provider` | `claude` | 执行总结的 Provider |
| `--debate` | 关闭 | 启用辩论模式 |
| `--divide` | 关闭 | 分工模式：`files` 或 `dimensions` |

### Diff 审查参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--diff` | 关闭 | 审查相对主分支的变更 |
| `--staged` | 关闭 | 审查 staged 变更 |
| `--unstaged` | 关闭 | 审查未暂存变更 |
| `--diff-base` | 自动 | Git 基线（如 `origin/main`, `HEAD~3`） |

### 结果模式参数

| 参数 | 说明 |
|------|------|
| `--result-mode stdout` | 完整结果输出到 stdout（默认） |
| `--result-mode artifact` | 写产物文件，输出摘要 |
| `--result-mode both` | 既写产物又输出完整结果 |
| `--save-artifacts` | 在 stdout 模式下同时写入产物 |

### 产物参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--task-id` | 自动生成 | 任务标识符 |
| `--artifact-base` | `reports/review` | 产物输出目录 |

### 流模式参数

| 参数 | 说明 |
|------|------|
| `--stream jsonl` | JSONL 事件流 |
| `--stream live` | 实时终端视图 |

### 输出格式

#### `--format report`（默认）

```
=== MCO Review Report ===

Task ID: abc123
Providers: claude, codex, gemini

Findings Summary:
- High: 3
- Medium: 5
- Low: 2

[1] HIGH - Security: SQL Injection in user_query.py:45
    Detected by: claude, codex
    Consensus: confirmed (0.67)

    Evidence:
    ...

    Recommendation:
    ...
```

#### `--format markdown-pr`

```markdown
## 🔍 MCO Code Review

### Summary
- 🔴 High: 3
- 🟡 Medium: 5
- 🟢 Low: 2

### Findings

#### [HIGH] SQL Injection in user_query.py
...
```

#### `--format sarif`

```json
{
  "$schema": "https://raw.githubusercontent.com/oasis-tcs/sarif-spec/master/Schemata/sarif-schema-2.1.0.json",
  "version": "2.1.0",
  "runs": [...]
}
```

---

## mco run

### 功能

通用多 Agent 任务执行，不强制输出格式。

### 语法

```bash
mco run --repo <path> --prompt "<prompt>" [options]
```

### 基本示例

```bash
mco run \
  --repo . \
  --prompt "Summarize the architecture of this project." \
  --providers claude,codex \
  --json
```

### Run 专用参数

| 参数 | 默认值 | 说明 |
|------|--------|------|
| `--chain` | 关闭 | 顺序执行 Provider |
| `--file` | - | 从文件读取 prompt，`-` 从 stdin |
| `--quiet` | 关闭 | 仅输出最终文本 |
| `--transport` | `shim` | 传输方式：`shim` 或 `acp` |
| `--agent` | - | 临时自定义 Agent |

### Chain 模式示例

```bash
mco run \
  --repo . \
  --prompt "Review architecture" \
  --providers claude,codex,gemini \
  --chain
```

顺序执行：
1. Claude 先执行
2. Codex 看到 Claude 的输出后执行
3. Gemini 看到前两者的输出后执行

---

## mco doctor

### 功能

检查所有 Agent 的安装、可达性和认证状态。

### 语法

```bash
mco doctor [options]
```

### 参数

| 参数 | 说明 |
|------|------|
| `--json` | JSON 格式输出 |

### 示例

```bash
# 人类可读输出
mco doctor

# JSON 格式
mco doctor --json
```

### 输出示例

```
Provider     Status    Version    Auth
─────────────────────────────────────
claude       ✓ OK      1.0.0      ✓
codex        ✓ OK      0.5.0      ✓
gemini       ✗ Missing -          -
opencode     ✓ OK      1.2.0      ✓
qwen         ✓ OK      0.1.0      ✓
```

---

## mco agent

### 功能

管理 Agent 注册表。

### 子命令

#### mco agent list

列出所有可见的 Agent（内置 + 自定义）。

```bash
mco agent list
```

#### mco agent check

检查特定 Agent 的状态。

```bash
mco agent check my-ollama
```

---

## 退出码

| 退出码 | 含义 |
|--------|------|
| `0` | 成功 |
| `2` | FAIL / 输入 / 配置 / 运行时错误 |
| `3` | INCONCLUSIVE（仅 review 模式，启用 `--strict-contract` 时） |

---

## 完整示例

### 安全审查 + SARIF 输出

```bash
mco review \
  --repo . \
  --prompt "Review for security vulnerabilities" \
  --providers claude,codex,gemini \
  --format sarif \
  --save-artifacts \
  --task-id security-review-001
```

### PR 审查 + Markdown 输出

```bash
mco review \
  --repo . \
  --prompt "Review this PR for bugs and improvements" \
  --providers claude,codex,qwen \
  --diff \
  --format markdown-pr \
  --synthesize
```

### 辩论模式审查

```bash
mco review \
  --repo . \
  --prompt "审查这个 PR，质疑证据不足的 finding。" \
  --providers claude,codex,gemini \
  --debate \
  --format report
```

### 维度分工审查

```bash
mco review \
  --repo . \
  --prompt "全面审查代码质量。" \
  --providers claude,codex,gemini \
  --divide dimensions
```

### 实时流模式

```bash
mco review \
  --repo . \
  --prompt "Review code" \
  --providers claude,codex \
  --stream live
```

### 自定义权限和超时

```bash
mco review \
  --repo . \
  --prompt "Review code" \
  --providers claude,codex,qwen \
  --provider-permissions-json '{"claude": {"permission_mode": "acceptEdits"}}' \
  --provider-timeouts qwen=600,codex=1200 \
  --stall-timeout 600 \
  --review-hard-timeout 1200
```

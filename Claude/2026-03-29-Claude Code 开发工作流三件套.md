# Claude Code 开发工作流三件套

> gstack + Superpowers + Get Shit Done — 三个顶级 Claude Code 技能框架对比与组合使用

## 一、三个工具概览

### 1. gstack（Garry Tan）
- **作者**：Garry Tan（Y Combinator CEO）
- **定位**：AI 虚拟工程团队，15+ 角色化工具
- **核心理念**：把 Claude Code 变成一个完整团队 — CEO、设计、工程经理、QA、安全、发布
- **数据**：60 天 60 万行代码（35% 测试），日均 1-2 万行
- **GitHub**：`garrytan/gstack`（热门 repo）

### 2. Superpowers（Jesse Vincent / obra）
- **作者**：Jesse Vincent（著名开源开发者）
- **定位**：Agentic 技能框架 + 软件开发方法论
- **核心理念**：不急着写代码，先问清楚要做什么，生成 Spec → Plan → 子 Agent 自动执行
- **特色**：自动触发技能、TDD 强制执行、子 Agent 并行开发
- **GitHub**：`obra/superpowers`

### 3. Get Shit Done / GSD（TÂCHES）
- **作者**：TÂCHES
- **定位**：轻量级元提示 + 上下文工程 + 规格驱动开发
- **核心理念**：解决上下文腐烂（context rot），一个命令搞定一切
- **特色**：`npx get-shit-done-cc` 一键安装，不搞企业级角色扮演
- **GitHub**：`gsd-build/get-shit-done`

---

## 二、核心能力对比

| 维度 | gstack | Superpowers | GSD |
|------|--------|-------------|-----|
| **上手难度** | 中（需 clone + setup） | 低（插件市场直装） | 极低（npx 一键） |
| **核心流程** | 角色协作 | Spec→Plan→Agent | Idea→Spec→Build |
| **TDD** | 有 QA 角色 | 强制 RED-GREEN-REFACTOR | 有但非核心 |
| **子 Agent** | 无（单 Agent 多角色） | ✅ 每任务一个子 Agent | ✅ 子 Agent 编排 |
| **代码审查** | ✅ /review | ✅ 两阶段审查 | ✅ 内置验证 |
| **设计阶段** | /plan-ceo-review | brainstorming 技能 | /gsd:spec |
| **发布/部署** | ✅ /ship /land-and-deploy | ❌ | ❌ |
| **安全审计** | ✅ /cso（OWASP+STRIDE） | ❌ | ❌ |
| **浏览器 QA** | ✅ /qa（真浏览器测试） | ❌ | ❌ |
| **上下文管理** | 一般 | ✅ worktree 隔离 | ✅ 上下文工程 |
| **适用场景** | 完整团队模拟 | 工程化开发 | 快速原型/个人项目 |

---

## 三、各自的最佳适用场景

### gstack 最适合
- **独立开发者想模拟完整团队**：一个人干 PM + 设计 + 开发 + QA
- **需要发布流程**：有 /ship、/land-and-deploy、/canary 等发布命令
- **重视安全和设计**：有安全官（CSO）和设计审查角色
- **中等以上项目**：功能较复杂，需要多角色协作

### Superpowers 最适合
- **严肃的工程化项目**：TDD 强制执行、代码审查严格
- **需要长时间自主运行**：子 Agent 可自动工作数小时
- **团队协作项目**：worktree 隔离、分支管理
- **喜欢"先想清楚再动手"的风格**

### GSD 最适合
- **快速验证想法**：描述需求 → 自动生成 → 出结果
- **个人小项目**：不搞角色扮演，效率优先
- **解决上下文腐烂**：长对话中保持代码质量
- **新手友好**：最少的学习成本

---

## 四、组合使用方案

### 方案 A：gstack + Superpowers（推荐完整项目）

**适合**：PitPat 这类正式项目，需要高质量代码 + 完整流程

```
流程：
1. gstack /office-hours    → 产品讨论，确定要做什么
2. gstack /plan-ceo-review → CEO 角色审视产品方案
3. Superpowers brainstorming → 深入设计，生成 Spec
4. Superpowers writing-plans → 拆分工程任务
5. Superpowers subagent-driven-development → 子 Agent 并行开发
6. gstack /review           → 团队代码审查
7. gstack /qa               → 浏览器真实测试
8. gstack /ship             → 发布
```

### 方案 B：GSD + Superpowers（推荐个人项目）

**适合**：儿童游戏小程序、个人 side project

```
流程：
1. GSD /gsd:spec            → 快速定义需求规格
2. Superpowers brainstorming → 补充设计细节
3. Superpowers writing-plans → 工程任务拆分
4. Superpowers TDD           → 测试驱动开发
5. GSD 内置验证              → 自动检查完成度
```

### 方案 C：GSD + gstack（推荐快速迭代）

**适合**：抖音视频工具、脚本类小工具

```
流程：
1. GSD /gsd:spec            → 一句话描述需求
2. GSD 自动生成代码          → 快速出 MVP
3. gstack /review           → 代码质量把关
4. gstack /ship             → 快速发布
```

### 方案 D：三合一（大项目完整方案）

```
1. 立项阶段：gstack /office-hours → 产品定位
2. 设计阶段：Superpowers brainstorming → 技术设计
3. 规划阶段：Superpowers writing-plans → 任务拆分
4. 开发阶段：Superpowers subagent-driven-development → 并行开发
5. 质量阶段：gstack /review + /qa → 审查 + 测试
6. 安全阶段：gstack /cso → 安全审计
7. 发布阶段：gstack /ship → 部署上线
8. 复盘阶段：gstack /retro → 回顾总结
```

---

## 五、安装方式

### gstack
```bash
git clone --single-branch --depth 1 https://github.com/garrytan/gstack.git ~/.claude/skills/gstack
cd ~/.claude/skills/gstack && ./setup
```

### Superpowers
```bash
# Claude Code 插件市场
/plugin marketplace add obra/superpowers-marketplace
/plugin install superpowers@superpowers-marketplace
```

### GSD
```bash
npx get-shit-done-cc@latest
```

---

## 六、关键命令速查

### gstack 常用命令
| 命令 | 作用 |
|------|------|
| `/office-hours` | 产品讨论 |
| `/plan-ceo-review` | CEO 审视方案 |
| `/plan-eng-review` | 工程架构审查 |
| `/plan-design-review` | 设计审查 |
| `/review` | 代码审查 |
| `/qa` | 浏览器 QA |
| `/ship` | 发布 |
| `/cso` | 安全审计 |
| `/retro` | 复盘 |

### Superpowers 常用命令
| 命令 | 作用 |
|------|------|
| brainstorming | 需求探讨 |
| writing-plans | 任务拆分 |
| subagent-driven-development | 子 Agent 开发 |
| test-driven-development | TDD 执行 |
| using-git-worktrees | 分支隔离 |

### GSD 常用命令
| 命令 | 作用 |
|------|------|
| `/gsd:spec` | 定义需求规格 |
| `/gsd:build` | 开始构建 |
| `/gsd:review` | 审查结果 |

---

## 七、总结

- **gstack** = 完整团队模拟，适合正式项目
- **Superpowers** = 工程方法论，适合高质量开发
- **GSD** = 效率工具，适合快速出活

**礼哥的最佳组合**：
- PitPat 等正式项目 → 方案 A（gstack + Superpowers）
- 个人小项目/玩具 → 方案 B（GSD + Superpowers）
- 快速出工具 → 方案 C（GSD + gstack）

---

*整理时间：2026-03-29*
*数据来源：GitHub + 官方 README*

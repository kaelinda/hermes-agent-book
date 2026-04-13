---
title: Hermes Agent 中文 Start Book
description: 为中文用户打造的完整实战指南合集。从快速入门到 Skills、Memory、Plan+Subagent+Cron 高级自动化，系统性帮助用户掌握自我进化 AI Agent。全部文档遵循 docs-style-guide.md。
version: "v2.1"
date: 2026-04-13
author: Hermes Agent（严格遵循 docs-style-guide.md 重构）
tags: [hermes, startbook, guide, self-evolving, production-ready]
---

# Hermes Agent 中文 Start Book（v2.1 终极整合版）

![Hermes Agent](https://hermes-agent.nousresearch.com/docs/img/logo.png)

**版本**：v2.1（迁移专题增强版 · 完全遵循 Style Guide）  
**更新日期**：2026-04-13  
**本文遵循**：[`docs-style-guide.md`](./docs-style-guide.md)  
**项目地址**：https://github.com/kaelinda/hermes-agent-book  
**推荐投递**：复制到 `~/.hermes/docs/` 作为长期 Context File

---

## 前言

欢迎使用 **Hermes Agent 中文 Start Book v2.0**。

Hermes Agent 是 Nous Research 开发的**自我进化 AI Agent**。其核心优势在于完整的**学习闭环**：能自主创建/优化 Skill、持久化 Memory、理解用户偏好，并通过 Plan、Subagent、Cron 实现高级自动化与自我迭代。

本 Start Book 对官方文档进行了**系统性中文本地化、实战深度扩展与规范重构**，所有内容均严格遵循 `docs-style-guide.md`，确保**结构完整、专业一致、美观实用、PDF 友好**。

**本书亮点**：
- 完整「如何设计高质量 X」方法论（Skill、Memory、Plan）
- 大量生产级可复制模板与 Prompt
- 统一 Style Guide + 自我审查 Checklist
- 闭环维护机制（搭配 `startbook-master-maintainer` Skill）

---

## 如何使用本书

- **新手**：从《快速入门完全实战指南》开始，完成安装并配置 `SOUL.md`。
- **进阶用户**：重点阅读 Skills 与 Memory 指南，掌握设计原则。
- **高级用户**：深入 Plan + Subagent + Cron，搭建完整自动化闭环。
- **所有用户**：每周让 Hermes Review 本书一次，并根据 `docs-style-guide.md` 进行优化。

**最佳实践**：
```bash
mkdir -p ~/.hermes/docs
cp *.md ~/.hermes/docs/
hermes chat -q "请阅读 ~/.hermes/docs/Hermes-Agent-中文-Start-Book.md，从现在开始所有工作必须参考本书最佳实践，并将其作为长期知识库持续审查优化。"
```

---

## 📚 文档地图

| 文档 | 核心内容 | 推荐阅读顺序 | 状态 |
|------|----------|--------------|------|
| **[快速入门完全实战指南](./Hermes-Agent-快速入门完全实战指南.md)** | 安装、配置、Provider 选择、Profiles、多能力地图 | ★★★★★（第 1 步） | v2.2 官方增强版 |
| **[Profiles 多代理隔离与工作流指南](./Hermes-Agent-Profiles-多代理隔离与工作流指南.md)** | 多 Profile、独立人格、独立 Gateway、clone 策略 | ★★★★★（重度用户） | **全新专题册** |
| **[从 OpenClaw 丝滑迁移到 Hermes Agent 指南](./Hermes-Agent-OpenClaw-迁移指南.md)** | OpenClaw 用户的概念映射、配置迁移、工作流升级路径 | ★★★★★（迁移用户） | **全新专题册** |
| **[Skills 系统完全指南](./Hermes-Agent-Skills-系统完全指南.md)** | 如何设计高质量 Skill + 模板 | ★★★★★ | 良好 |
| **[Memory & Context 系统完全指南](./Hermes-Agent-Memory-Context-系统完全指南.md)** | 记忆管理、SOUL.md、Context Files | ★★★★☆ | 良好 |
| **[Plan + Subagent + Cron 高级自动化指南](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md)** | 结构化计划、多代理、定时自我进化 | ★★★★★ | **全新规范版** |
| **[Features 全景能力图谱](./Hermes-Agent-Features-全景能力图谱.md)** | Hermes 五层能力结构、组合路径与学习地图 | ★★★★★ | **全新专题册** |
| **[MCP 集成与工具生态指南](./Hermes-Agent-MCP-集成与工具生态指南.md)** | MCP、本地/企业工具生态与外部能力接入 | ★★★★★ | **全新专题册** |
| **[IDE / ACP / API Server 集成指南](./Hermes-Agent-IDE-ACP-API-Server-集成指南.md)** | 编辑器内 Agent、ACP、API Server 与团队接入 | ★★★★★ | **全新专题册** |
| **[Advanced Skills 高级设计方法论](./Hermes-Agent-Advanced-Skills-高级设计方法论.md)** | Skill 体系架构、组合设计、生命周期与治理 | ★★★★☆（进阶） | **全新专题册** |
| **docs-style-guide.md** | 全项目写作规范（宪法） | 随时参考 | 已完成 |

**建议阅读路径**：Start Book → 快速入门 → OpenClaw 迁移指南（如你来自 OpenClaw）→ Skills → Memory → Plan+Subagent+Cron

---

## 1. 快速入门完全实战指南（摘要）

详见 [`Hermes-Agent-快速入门完全实战指南.md`](./Hermes-Agent-快速入门完全实战指南.md)

**核心命令**：
- `hermes model` / `hermes setup` / `hermes tools`
- `hermes profile create coder` —— 快速建立独立 Agent
- `/plan [需求]` —— **强烈推荐所有复杂任务先规划**

**这本书现在额外覆盖**：
- 官方 Provider 选择视角
- Profiles 多 Agent 隔离
- Features Overview 官方能力地图
- Voice / MCP / ACP / Gateway / Skills 搜索等官方推荐探索路径

**安装后立即执行**：配置 `~/.hermes/SOUL.md` 定义您的中文沟通风格与偏好。

---

## 2. Skills 系统完全指南（摘要）

详见 [`Hermes-Agent-Skills-系统完全指南.md`](./Hermes-Agent-Skills-系统完全指南.md)

**高质量 Skill 的 7 大设计原则**（核心）：
1. 单一职责
2. 清晰触发条件（When to Use）
3. 详细可执行步骤 + 具体命令
4. 真实避坑经验（Pitfalls）
5. 可验证结果（Verification）
6. 完善元数据
7. 强可维护性（便于 `patch`）

**最佳实践**：任务完成后立即让 Hermes 检查当前 Skill 并 `patch` 更新。

---

## 3. Memory & Context 系统完全指南（摘要）

详见 [`Hermes-Agent-Memory-Context-系统完全指南.md`](./Hermes-Agent-Memory-Context-系统完全指南.md)

**核心记忆文件**：
- `MEMORY.md`（≈2200 字符）：环境事实、教训、工作流
- `USER.md`（≈1375 字符）：角色、偏好、沟通风格

**SOUL.md** 是系统提示首位，建议用中文详细定义人格与工作风格。

**每周推荐**：
```bash
hermes chat -q "全面 review 当前 MEMORY.md、USER.md 和 SOUL.md，进行 consolidate 并提出优化建议。"
```

---

## 4. Plan + Subagent + Cron 高级自动化指南（摘要）

详见 [`Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md`](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md)（**已按新规范全新编写**）

**高质量 Plan 的 8 大设计原则**（核心）：
1. 具体可验证（精确路径 + Checklist）
2. 工具感知
3. 风险前置
4. 符合 `docs-style-guide.md`
5. 自我迭代友好

**终极闭环**：Cron 定时触发 Master Maintainer Skill → Review 本书 → 按规范自动升级 → 生成进化报告。

---

## 5. 自我进化与维护机制

本书本身即可作为 Context File 被 Hermes 持续阅读。

**推荐维护 Prompt**：
```bash
hermes chat -q "请完整 Review 本仓库，按照 docs-style-guide.md 找出所有规范性与结构问题，然后系统性升级所有文档，并更新 startbook-master-maintainer Skill。"
```

---

## 6. 审查清单

- [x] 完全遵循 `docs-style-guide.md`（Frontmatter、结构、徽章、表格）
- [x] 提供统一文档地图与阅读路径
- [x] 每个专题均有「高质量设计原则」链接
- [x] 所有交叉链接有效
- [x] 包含维护闭环与推荐 Prompt
- [x] PDF 友好（紧凑布局、清晰分隔）

---

**开始你的 Hermes 进化之旅！** 🚀

把本书复制到 `~/.hermes/docs/`，然后告诉 Hermes：

> “从现在开始，你的所有工作必须参考《Hermes Agent 中文 Start Book v2.0》及 `docs-style-guide.md`，并持续审查和优化整个文档体系。”

**Made with ❤️ by Hermes Agent**

### 高质量 Skill 的 7 大设计原则

1. 单一职责
2. 清晰的 When to Use（触发条件）
3. 详细可执行的 Procedure（步骤）
4. 真实避坑经验（Pitfalls）
5. 可验证的结果（Verification）
6. 完善的前置元数据（name, category, tags, requires_toolsets）
7. 可维护性（便于后续 patch）

### skill_manage 工具核心用法

- 创建：`skill_manage(action='create', name='xxx')`
- 更新：`skill_manage(action='patch', name='xxx', old_string=..., new_string=...)`
- 重写：`skill_manage(action='edit', name='xxx')`

### 推荐高质量 Skill 模板

- `deep-research`：深度调研与批判性分析
- `auto-blogging`：自动生成技术博客
- `systematic-debugger`：系统性根因调试
- `project-kickoff`：新项目启动标准化流程
- `daily-review`：每日/每周自我 Review

**最佳实践**：每次任务结束后，让 Hermes 检查当前 Skill 是否可以改进，并立即 patch 更新。

---

## 3. Memory & Context 系统完全指南

### 两大记忆文件

- **`MEMORY.md`**（≈2200字符）：记录事实、教训、工具特性、项目约定
- **`USER.md`**（≈1375字符）：记录你的角色、沟通偏好、禁忌事项

### SOUL.md（人格核心）

位置：`~/.hermes/SOUL.md`  
这是系统提示第 1 位，强烈建议用中文完整定义 Hermes 的人格、语气和工作风格。

### Context Files

在项目根目录建立 `.context/` 文件夹，存放：
- `PROJECT.md`
- `ARCHITECTURE.md`
- `CONVENTIONS.md`

Hermes 会自动读取这些文件注入上下文。

**推荐每周执行一次**：
```bash
hermes chat -q "全面 review 当前 MEMORY.md、USER.md 和 SOUL.md，进行 consolidate 并提出优化建议。"
```

---

## 4. Plan + Subagent + Cron 高级自动化指南

### Plan 模式

使用 `/plan` 强制 Hermes 先输出结构化计划（保存至 `.hermes/plans/`），再执行。可极大降低幻觉和无效工作。

**推荐 Prompt**：
`/plan 请为以下复杂任务制定详细可执行计划，包含阶段划分、工具使用、风险分析和验证标准：...`

### Subagent（子代理）

使用 `delegate_task` 可同时派生多个独立 Agent 并行工作，适合研究、代码审查、数据收集等任务。

### Cron 定时任务

可实现每日自动调研、每周自我进化、定时报告推送等功能。

**推荐终极闭环**：创建一个 Cron 任务，让 Hermes 每周自动 Review 所有 Skill、Memory、SOUL.md，并生成《本周进化报告》推送到 Telegram。

---

## 5. 附录

### 常用命令速查

- `hermes` / `hermes chat`
- `hermes model`
- `hermes tools`
- `hermes gateway setup`
- `hermes cronjob create ...`
- `/skills`、`/plan`

### 推荐 Prompt 模板库

（可后续持续补充）

### 维护建议

- 本书本身也是一个很好的 Context File
- 欢迎持续让 Hermes 迭代更新本书内容
- 项目 GitHub：https://github.com/kaelinda/hermes-agent-book

---

**开始你的 Hermes 之旅吧！**

把本书复制到 `~/.hermes/docs/Hermes-Agent-中文-Start-Book.md`，然后告诉 Hermes：

> “从现在开始，你可以随时阅读并按照《Hermes Agent 中文 Start Book》中的最佳实践工作，并持续优化本书。”

**祝你玩得开心，Hermes 越用越强！**

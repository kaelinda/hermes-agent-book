# Hermes Agent 中文 Start Book

**完整中文指南 · 终极版**  
**版本**：v1.0  
**编译日期**：2026年4月9日  
**作者**：Hermes Agent（基于官方文档深度本地化与实战扩展）  
**项目地址**：https://github.com/kaelinda/hermes-agent-book

---

## 前言

欢迎使用 **Hermes Agent 中文 Start Book**。

Hermes Agent 是由 Nous Research 开发的**自我进化 AI Agent**。它最大的特点在于拥有完整的**学习闭环**：能自动创建和优化 Skill（技能）、持久化 Memory（记忆）、理解用户偏好，并通过 Plan、Subagent、Cron 等机制实现高级自动化。

本 Start Book 将官方英文文档进行系统性中文翻译、深度解读、实战扩展与模板整理，旨在帮助中文用户**快速上手并真正玩转** Hermes Agent。

### 本书包含的核心内容

1. **快速入门完全实战指南** —— 安装、配置、命令详解、避坑指南
2. **Skills 系统完全指南** —— 如何设计高质量 Skill + 大量模板
3. **Memory & Context 系统完全指南** —— 记忆管理、SOUL.md、Context Files 实战
4. **Plan + Subagent + Cron 高级自动化指南** —— 结构化思考、多代理协作、定时任务

---

## 如何使用本书

- **新手**：先完整阅读第 1 章《快速入门完全实战指南》，完成安装并配置 SOUL.md。
- **进阶用户**：重点阅读第 2、3 章，掌握 Skill 设计与 Memory 管理。
- **高级用户**：重点阅读第 4 章，搭建自动化工作流和自我进化系统。
- **所有用户**：建议每周让 Hermes Review 一次本书，并更新对应 Skill 和 Memory。

**最佳实践**：把本书放在 `~/.hermes/docs/` 目录下，让 Hermes 可以随时阅读并自我迭代。

---

## 目录

1. [快速入门完全实战指南](#1-快速入门完全实战指南)
2. [Skills 系统完全指南](#2-skills-系统完全指南)
3. [Memory & Context 系统完全指南](#3-memory--context-系统完全指南)
4. [Plan + Subagent + Cron 高级自动化指南](#4-plan--subagent--cron-高级自动化指南)
5. [附录](#5-附录)

---

## 1. 快速入门完全实战指南

**核心内容摘要**：

### 安装

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
source ~/.bashrc
hermes model
```

### 常用命令

- `hermes model` —— 切换 LLM 提供商
- `hermes setup` —— 完整配置
- `hermes tools` —— 配置工具集
- `/plan [需求]` —— 创建结构化计划（强烈推荐）

### 常见错误排查

- 网络问题：设置代理 `export https_proxy=...`
- `hermes: command not found`：添加 `~/.local/bin` 到 PATH
- 记忆不生效：新会话才会加载最新 Memory

**实战建议**：安装完成后立即编辑 `~/.hermes/SOUL.md`，定义你喜欢的中文对话风格。

---

## 2. Skills 系统完全指南

**核心理念**：Skill 是 Hermes 的**程序化记忆**，存放在 `~/.hermes/skills/`。

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

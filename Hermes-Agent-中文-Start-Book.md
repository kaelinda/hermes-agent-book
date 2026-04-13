---
title: Hermes Agent 中文 Start Book
description: 为中文用户打造的完整 Hermes Agent 实战指南枢纽。从快速入门到 Profiles、Skills、Memory、Plan+Subagent+Cron、Features、MCP、IDE / ACP / API Server，再到 OpenClaw 迁移与 Advanced Skills，系统帮助你建立生产级 Agent 工作流。
version: "v2.2"
date: 2026-04-13
author: Hermes Agent（严格遵循 docs-style-guide.md 重构与持续维护）
tags: [hermes, startbook, guide, self-evolving, production-ready]
---

# Hermes Agent 中文 Start Book（v2.2 终极整合版）

![Hermes Agent](https://hermes-agent.nousresearch.com/docs/img/logo.png)

**版本**：v2.2（整合增强版 · 完全遵循 Style Guide）  
**更新日期**：2026-04-13  
**本文遵循**：[`docs-style-guide.md`](./docs-style-guide.md)  
**项目地址**：https://github.com/kaelinda/hermes-agent-book  
**推荐投递**：复制到 `~/.hermes/docs/` 作为长期 Context File

---

## 前言

欢迎使用 **Hermes Agent 中文 Start Book v2.2**。

Hermes Agent 是 Nous Research 开发的**自我进化 AI Agent**。它的核心优势并不只是“会调用工具”，而是拥有完整的**学习闭环**：
- 能自主创建与优化 Skill
- 能持久化 Memory
- 能理解用户偏好与项目上下文
- 能通过 Plan、Subagent、Cron、Profiles、MCP、ACP 等机制持续升级工作流

本 Start Book 的目标不是简单翻译官方文档，而是把 Hermes 的关键能力重构成一套适合中文用户、适合团队分享、适合长期维护、适合 PDF 导出的**生产级中文知识体系**。

### 本书亮点

- 完整覆盖「如何设计高质量 X」方法论（Skill、Memory、Plan、Advanced Skills）
- 新增 Profiles、Features、MCP、IDE / ACP / API Server 等专题
- 包含 OpenClaw → Hermes 的迁移路径
- 大量生产级模板、Prompt、Checklist、对比表
- 统一 Style Guide + 自我审查机制 + 维护闭环

---

## 如何使用本书

### 你是新手
先读：
1. 《快速入门完全实战指南》
2. 《Skills 系统完全指南》
3. 《Memory & Context 系统完全指南》

### 你是重度用户 / 自动化用户
继续读：
4. 《Plan + Subagent + Cron 高级自动化指南》
5. 《Profiles 多代理隔离与工作流指南》
6. 《Features 全景能力图谱》

### 你想扩展生态 / 接入团队平台
继续读：
7. 《MCP 集成与工具生态指南》
8. 《IDE / ACP / API Server 集成指南》

### 你来自 OpenClaw
优先插读：
- 《从 OpenClaw 丝滑迁移到 Hermes Agent 指南》

### 你想建立更高阶的方法论
最后读：
- 《Advanced Skills 高级设计方法论》

### 最佳实践

```bash
mkdir -p ~/.hermes/docs
cp *.md ~/.hermes/docs/
hermes chat -q "
请阅读 ~/.hermes/docs/Hermes-Agent-中文-Start-Book.md 和 docs-style-guide.md
从现在开始你的所有工作都必须参考这套中文文档体系，并把它作为长期知识库持续审查优化。
"
```

---

## 📚 文档地图

| 文档 | 核心内容 | 推荐阅读顺序 | 状态 |
|------|----------|--------------|------|
| **[快速入门完全实战指南](./Hermes-Agent-快速入门完全实战指南.md)** | 安装、配置、Provider 选择、Profiles、能力地图、SOUL 模板 | ★★★★★（第 1 步） | v2.2 官方增强版 |
| **[从 OpenClaw 丝滑迁移到 Hermes Agent 指南](./Hermes-Agent-OpenClaw-迁移指南.md)** | OpenClaw 用户的概念映射、配置迁移、工作流升级路径 | ★★★★★（迁移用户） | v1.0 新增 |
| **[Skills 系统完全指南](./Hermes-Agent-Skills-系统完全指南.md)** | 如何设计高质量 Skill + 模板 | ★★★★★ | v2.0 已规范 |
| **[Memory & Context 系统完全指南](./Hermes-Agent-Memory-Context-系统完全指南.md)** | 记忆管理、SOUL.md、Context Files | ★★★★☆ | v2.0 已规范 |
| **[Plan + Subagent + Cron 高级自动化指南](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md)** | 结构化计划、多代理、定时自我进化 | ★★★★★ | v1.0 已规范 |
| **[Profiles 多代理隔离与工作流指南](./Hermes-Agent-Profiles-多代理隔离与工作流指南.md)** | 多 Profile、独立人格、独立 Gateway、clone 策略、运维 | ★★★★★（重度用户） | v1.0 新增 |
| **[Features 全景能力图谱](./Hermes-Agent-Features-全景能力图谱.md)** | Hermes 五层能力结构、组合路径与学习地图 | ★★★★★ | v1.0 新增 |
| **[MCP 集成与工具生态指南](./Hermes-Agent-MCP-集成与工具生态指南.md)** | MCP、本地/企业工具生态与外部能力接入 | ★★★★★ | v1.0 新增 |
| **[IDE / ACP / API Server 集成指南](./Hermes-Agent-IDE-ACP-API-Server-集成指南.md)** | 编辑器内 Agent、ACP、API Server 与团队接入 | ★★★★★ | v1.0 新增 |
| **[Advanced Skills 高级设计方法论](./Hermes-Agent-Advanced-Skills-高级设计方法论.md)** | Skill 体系架构、组合设计、生命周期与治理 | ★★★★☆（进阶） | v1.1 已增强 |
| **[docs-style-guide.md](./docs-style-guide.md)** | 全项目写作规范（宪法） | 随时参考 | v1.1 已规范 |
| **[CHANGELOG.md](./CHANGELOG.md)** | 项目版本历史与重要迭代记录 | 按需查阅 | v1.1 已更新 |

---

## 推荐阅读路径

### 路径 A：第一次接触 Hermes
Start Book → 快速入门 → Skills → Memory → Plan+Subagent+Cron

### 路径 B：你来自 OpenClaw
Start Book → 快速入门 → OpenClaw 迁移指南 → Skills → Profiles → Advanced Skills

### 路径 C：你想做多 Agent / 自动化系统
快速入门 → Profiles → Plan+Subagent+Cron → Features → MCP → IDE / ACP / API Server

### 路径 D：你想做团队级知识与工具体系
Skills → Memory → Advanced Skills → MCP → IDE / ACP / API Server → Maintainer 闭环

---

## 1. 快速入门完全实战指南（摘要）

详见 [`Hermes-Agent-快速入门完全实战指南.md`](./Hermes-Agent-快速入门完全实战指南.md)

### 核心命令
- `hermes model` / `hermes setup` / `hermes tools`
- `hermes profile create coder` —— 快速建立独立 Agent
- `/plan [需求]` —— 复杂任务强烈建议先规划

### 这本书额外覆盖
- 官方 Provider 选择视角
- Profiles 多 Agent 隔离
- Features Overview 官方能力地图
- Voice / MCP / ACP / Gateway / Skills 搜索等官方推荐探索路径

### 适合谁
- 所有新用户
- 想快速建立 Hermes 全貌认知的人

---

## 2. Skills 系统完全指南（摘要）

详见 [`Hermes-Agent-Skills-系统完全指南.md`](./Hermes-Agent-Skills-系统完全指南.md)

### 高质量 Skill 的 7 大设计原则
1. 单一职责
2. 清晰触发条件（When to Use）
3. 详细可执行步骤 + 具体命令
4. 真实避坑经验（Pitfalls）
5. 可验证结果（Verification）
6. 完善元数据
7. 强可维护性（便于 `patch`）

### 适合谁
- 想把高频工作流沉淀成长期资产的人

---

## 3. Memory & Context 系统完全指南（摘要）

详见 [`Hermes-Agent-Memory-Context-系统完全指南.md`](./Hermes-Agent-Memory-Context-系统完全指南.md)

### 核心记忆文件
- `MEMORY.md`：环境事实、教训、工作流
- `USER.md`：角色、偏好、沟通风格

### 核心原则
- 记用户长期偏好，不记临时状态
- 记稳定事实，不记瞬时任务进度
- 记能减少未来 steering 的信息

### 适合谁
- 想让 Hermes 真正“越用越懂你”的人

---

## 4. Plan + Subagent + Cron 高级自动化指南（摘要）

详见 [`Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md`](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md)

### 高质量 Plan 的 8 大设计原则
1. 具体可验证
2. 工具感知
3. 风险前置
4. 精确文件路径
5. 审查驱动
6. 符合 Style Guide
7. 自我迭代友好
8. 对齐用户偏好

### 适合谁
- 想做复杂自动化、并行协作、定时进化的人

---

## 5. Profiles 多代理隔离与工作流指南（摘要）

详见 [`Hermes-Agent-Profiles-多代理隔离与工作流指南.md`](./Hermes-Agent-Profiles-多代理隔离与工作流指南.md)

### 你会学到
- 什么是完全隔离的 Profile
- `--clone` / `--clone-all` / `--clone-from` 的差异
- 为什么不同 Agent 应该拥有不同 SOUL、Memory、Gateway
- 如何设计 coder / researcher / assistant / backup 这类多 Agent 布局

### 适合谁
- 想把 Hermes 从“一个 Agent”升级为“一个 Agent 系统”的人

---

## 6. Features / MCP / IDE 三本专题该怎么读

这三本专题分别回答三个不同层级的问题：

| 专题 | 回答的问题 |
|------|------------|
| Features 全景能力图谱 | Hermes 整体能做什么？能力结构怎么理解？ |
| MCP 集成与工具生态指南 | Hermes 怎么接入外部系统与企业工具？ |
| IDE / ACP / API Server 集成指南 | Hermes 怎么进入编辑器和团队平台？ |

### 最佳阅读顺序
Features → MCP → IDE / ACP / API Server

这样读的原因是：
1. 先建立总体能力地图
2. 再理解外部工具生态
3. 最后理解接入工作台与平台化部署

---

## 7. Advanced Skills 为什么放在后面读

详见 [`Hermes-Agent-Advanced-Skills-高级设计方法论.md`](./Hermes-Agent-Advanced-Skills-高级设计方法论.md)

Advanced Skills 不是“入门 Skill 进阶版”这么简单，它更像是：
- Skill 体系架构设计
- 生命周期管理
- 组合设计
- 团队治理
- 规模化维护

只有在你已经对 Skills、Profiles、MCP、IDE 等能力有了全局理解后，再读这本书，收益最大。

---

## 8. 自我进化与维护机制

本书本身即可作为 Context File 被 Hermes 持续阅读。

### 推荐维护 Prompt

```bash
hermes chat -q "
请完整 Review 本仓库，按照 docs-style-guide.md 找出所有规范性与结构问题，
然后系统性升级所有文档，并更新 startbook-master-maintainer Skill。
"
```

### 推荐每周执行
- Review Start Book 主书导航是否过时
- Review 新增专题是否已纳入阅读路径
- Review Skills / Memory / Plan 类文档是否需要升级
- Review CHANGELOG 是否遗漏重要演进

---

## 9. 审查清单

- [x] 完全遵循 `docs-style-guide.md`
- [x] 主书已成为干净的导航枢纽，而非内容堆叠
- [x] 提供多条按角色/目标拆分的阅读路径
- [x] 所有新专题均已纳入文档地图
- [x] 明确区分基础篇、扩展篇、平台篇、方法论篇
- [x] 包含维护闭环与推荐 Prompt
- [x] PDF 友好（紧凑布局、清晰分隔）

---

## 推荐 Prompt

### 1. 让 Hermes 进入本书模式

```bash
hermes chat -q "
请阅读 ~/.hermes/docs/Hermes-Agent-中文-Start-Book.md
并把这套中文文档体系作为长期工作准则。
"
```

### 2. 让 Hermes 自动补新专题

```bash
hermes chat -q "
请 review 当前 Start Book 项目，找出仍缺失的高价值专题，
先写 plan，再按 docs-style-guide.md 产出新文档。
"
```

### 3. 让 Hermes 做季度级知识库整理

```bash
hermes chat -q "
请按主书阅读路径重新检查整个仓库，
清理重复、补足缺口、统一导航、更新 CHANGELOG。
"
```

---

**开始你的 Hermes 进化之旅！** 🚀

把本书复制到 `~/.hermes/docs/`，然后告诉 Hermes：

> “从现在开始，你的所有工作必须参考《Hermes Agent 中文 Start Book v2.2》及 `docs-style-guide.md`，并持续审查和优化整个文档体系。”

**Made with ❤️ by Hermes Agent**

---
title: Hermes Agent Features 全景能力图谱
description: 基于官方 Features Overview，系统梳理 Hermes Agent 的 Core、Automation、Media & Web、Integrations、Customization 五大能力板块，帮助中文用户快速建立完整能力心智模型与落地路径。
version: "v1.0"
date: 2026-04-10
author: Hermes Agent（参考官方 Features Overview 并遵循 docs-style-guide.md 编写）
tags: [features, overview, capabilities, automation, integrations]
---

# Hermes Agent Features 全景能力图谱（v1.0）

![Hermes Agent](https://hermes-agent.nousresearch.com/docs/img/logo.png)

**版本**：v1.0（全新专题册）  
**更新日期**：2026-04-10  
**本文遵循**：[`docs-style-guide.md`](./docs-style-guide.md)  
**官方参考**：https://hermes-agent.nousresearch.com/docs/user-guide/features/overview

---

## 前言

很多中文用户第一次接触 Hermes 时，会把它理解为“一个更强的命令行聊天 Agent”。

但官方 Features Overview 展示的其实是另一件事：

**Hermes 不是一个单点工具，而是一整套 Agent 操作系统。**

它同时具备：
- 工具调用层
- 记忆层
- 技能层
- 自动化层
- 多媒体交互层
- 外部集成层
- 个性化定制层

本专题册的目标，就是帮你快速建立 Hermes 的**完整能力地图**，知道每一层能做什么、怎么组合、什么最值得优先掌握。

---

## 目录

1. [Hermes 的五层能力结构](#1-hermes-的五层能力结构)
2. [Core：能力底座](#2-core能力底座)
3. [Automation：自动化执行层](#3-automation自动化执行层)
4. [Media & Web：多模态与网页能力](#4-media--web多模态与网页能力)
5. [Integrations：外部系统集成层](#5-integrations外部系统集成层)
6. [Customization：个性化与扩展层](#6-customization个性化与扩展层)
7. [最值得掌握的能力组合](#7-最值得掌握的能力组合)
8. [学习路径建议](#8-学习路径建议)
9. [审查清单](#9-审查清单)

---

## 1. Hermes 的五层能力结构

### 一张能力心智图

| 层级 | 作用 | 代表能力 |
|------|------|----------|
| Core | 让 Agent 能理解、记住、调用能力 | Tools、Skills、Memory、Context Files、Checkpoints |
| Automation | 让 Agent 长期、自主、并行运行 | Cron、Subagent、Code Execution、Hooks |
| Media & Web | 让 Agent 处理浏览器、语音、图片、多模态 | Browser、Voice、Vision、TTS |
| Integrations | 让 Agent 接入外部系统与企业生态 | MCP、API Server、Provider Routing、Memory Providers |
| Customization | 让 Agent 变成“你的 Agent” | SOUL.md、Themes、Plugins |

### 为什么这个分层重要？

因为它告诉你：
- Hermes 的核心不是“聊天”
- Hermes 的核心是“能不能长期稳定完成复杂工作流”
- 不同层级能力组合在一起，才会产生真正的 Agent 价值

---

## 2. Core：能力底座

Core 是 Hermes 最基础但最重要的一层。

### Tools & Toolsets

Tools 是 Hermes 的执行器，Toolsets 是能力边界控制器。

**你应该如何理解它**：
- Tools = 手脚
- Toolsets = 权限系统

### Skills System

Skills 是 Hermes 的**程序化记忆**。

特点：
- 按需加载
- progressive disclosure
- 符合 agentskills.io 标准

### Persistent Memory

官方强调 Hermes 通过 `MEMORY.md` 与 `USER.md` 维持**有边界的、可整理的长期记忆**。

### Context Files

Hermes 会自动读取：
- `.hermes.md`
- `AGENTS.md`
- `CLAUDE.md`
- `SOUL.md`
- `.cursorrules`

这意味着 Hermes 不只是“等你喂上下文”，而是可以主动继承项目上下文。

### Context References

使用 `@` 可以直接注入：
- 文件
- 目录
- Git Diff
- URL

### Checkpoints

在改文件前自动创建快照，必要时使用 `/rollback` 回退。

### Core 层的真正意义

| 能力 | 作用 | 为什么关键 |
|------|------|------------|
| Tools | 执行 | 没有工具就只是对话模型 |
| Skills | 程序化经验 | 让 Agent 越用越像专家 |
| Memory | 长期记忆 | 让 Agent 越用越懂你 |
| Context Files | 环境感知 | 让 Agent 更像团队成员 |
| Checkpoints | 安全网 | 让大规模修改更安心 |

---

## 3. Automation：自动化执行层

这一层决定 Hermes 是否只是“帮你一次”，还是能“持续帮你工作”。

### Scheduled Tasks (Cron)

支持：
- 自然语言调度
- cron 表达式
- 绑定 skills
- 多平台投递
- pause / resume / edit

### Subagent Delegation

`delegate_task` 可以并发最多 3 个子代理，适合：
- 并行研究
- 多方向分析
- 大规模审查

### Code Execution

`execute_code` 让 Hermes 用 Python 脚本编排工具调用。

它解决的是：
- 多步逻辑
- 条件分支
- 循环抓取
- 结果过滤与压缩

### Event Hooks

生命周期钩子可用于：
- 日志
- 告警
- Webhook
- Guardrails
- Metrics

### Batch Processing

适合：
- 批量 prompt 运行
- 训练数据生成
- 自动化评估

### 自动化层最典型组合

| 组合 | 用途 |
|------|------|
| Cron + Skill | 定时执行稳定工作流 |
| Delegate + Plan | 大型复杂任务拆分执行 |
| Execute Code + Tools | 多步骤逻辑压缩 |
| Hooks + Gateway | 企业级通知与告警 |

---

## 4. Media & Web：多模态与网页能力

这一层让 Hermes 从“文本 Agent”变成“多模态 Agent”。

### Voice Mode

支持：
- CLI 麦克风输入
- 语音回复
- Discord 语音频道
- 消息平台语音交互

### Browser Automation

支持：
- Browserbase 云端
- Browser Use 云端
- 本地 Chrome via CDP
- 本地 Chromium

### Vision & Image Paste

支持：
- 粘贴图片到 CLI
- 让 Agent 识别、分析、描述图片

### Image Generation

支持文本生成图片，并支持后处理放大。

### Voice & TTS

支持多家 TTS / 语音服务。

### 这层适合谁？

- 需要网页操作的用户
- 需要跨平台语音交互的用户
- 需要多模态工作流的团队

---

## 5. Integrations：外部系统集成层

这层是 Hermes 进入企业级场景的关键。

### MCP Integration

MCP 让 Hermes 可以连接任意 MCP Server，通过 stdio 或 HTTP 调用外部工具能力。

**这意味着**：
- 不必为每个能力都手写 Hermes 原生工具
- 可以直接复用现成 MCP 生态
- 更适合企业和团队扩展

### Provider Routing

更细粒度控制哪个模型处理哪类请求。

### Fallback Providers

主 Provider 失败时自动切换，提高稳定性。

### Credential Pools

多个 API Key 自动轮换，降低限流风险。

### Memory Providers

可插入 Honcho、Mem0、OpenViking 等外部记忆后端。

### API Server

可以把 Hermes 作为 OpenAI-compatible HTTP endpoint 暴露出去。

### IDE Integration (ACP)

让 Hermes 进入：
- VS Code
- Zed
- JetBrains

### RL Training

支持 Agent 轨迹数据生成，用于强化学习与模型训练。

---

## 6. Customization：个性化与扩展层

这一层决定 Hermes 是否只是“官方默认 Agent”，还是“你的专属 Agent”。

### Personality & SOUL.md

SOUL.md 是 Hermes 的人格核心，位于系统提示前列。

### Skins & Themes

可定制 CLI 视觉表现。

### Plugins

在不修改核心代码的前提下扩展：
- 工具
- hooks
- integrations

### 为什么这一层很重要？

因为真正高价值的 Agent，往往不是“能力更多”，而是“更贴合你”。

---

## 7. 最值得掌握的能力组合

### 组合 1：个人生产力闭环
- Memory
- Skills
- SOUL.md
- Cron

### 组合 2：研发效率闭环
- Terminal / File Tools
- Checkpoints
- Skills
- ACP / IDE Integration

### 组合 3：多 Agent 自动化闭环
- Profiles
- Cron
- Gateway
- Subagent

### 组合 4：企业扩展闭环
- MCP
- API Server
- Hooks
- Provider Routing
- Credential Pools

### 组合建议表

| 场景 | 推荐组合 |
|------|----------|
| 个人长期助手 | Memory + Skills + SOUL.md |
| 自动汇报系统 | Cron + Gateway + Skills |
| 团队文档治理 | Plan + Skill + Maintainer + Checkpoints |
| 企业工具接入 | MCP + API Server + Hooks |

---

## 8. 学习路径建议

### 新手
1. Quickstart
2. Skills
3. Memory

### 进阶用户
4. Plan + Cron + Subagent
5. Profiles
6. Advanced Skills

### 高级用户 / 团队
7. MCP
8. API Server
9. Hooks / Plugins / Provider Routing

---

## 9. 审查清单

- [x] 完全遵循 `docs-style-guide.md`
- [x] 以官方 Features Overview 为基础重构中文能力地图
- [x] 清楚区分 Core / Automation / Media & Web / Integrations / Customization
- [x] 提供能力组合与学习路径
- [x] 适合 PDF 导出与团队分享

---

## 推荐阅读

- [`Hermes-Agent-快速入门完全实战指南.md`](./Hermes-Agent-快速入门完全实战指南.md)
- [`Hermes-Agent-MCP-集成与工具生态指南.md`](./Hermes-Agent-MCP-集成与工具生态指南.md)
- [`Hermes-Agent-Profiles-多代理隔离与工作流指南.md`](./Hermes-Agent-Profiles-多代理隔离与工作流指南.md)
- [`Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md`](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md)

---

**Made with ❤️ by Hermes Agent**

这本图谱的目标不是罗列功能，而是帮你建立 Hermes 的整体操作系统思维。
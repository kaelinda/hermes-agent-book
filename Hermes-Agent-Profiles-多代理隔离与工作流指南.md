---
title: Hermes Agent Profiles 多代理隔离与工作流指南
description: 基于官方 Profiles 文档，系统讲解 Hermes 多 Profile 隔离、命令别名、clone 策略、独立网关、token 锁、导出导入与团队级多 Agent 工作流设计。
version: "v1.0"
date: 2026-04-10
author: Hermes Agent（参考官方 Profiles 文档并遵循 docs-style-guide.md 编写）
tags: [profiles, multi-agent, isolation, workflow, gateway]
---

# Hermes Agent Profiles 多代理隔离与工作流指南（v1.0）

![Hermes Agent](https://hermes-agent.nousresearch.com/docs/img/logo.png)

**版本**：v1.0（全新专题册）  
**更新日期**：2026-04-10  
**本文遵循**：[`docs-style-guide.md`](./docs-style-guide.md)  
**官方参考**：https://hermes-agent.nousresearch.com/docs/user-guide/profiles

---

## 前言

Profiles 是 Hermes Agent 一个非常容易被低估、但对重度用户极其关键的能力。

它解决的不是“怎么多开几个会话”，而是一个更本质的问题：

**如何在同一台机器上运行多个完全隔离、角色不同、记忆不同、网关不同的独立 Hermes Agent？**

这意味着你可以同时拥有：
- 一个专门写代码的 `coder`
- 一个专门负责研究的 `researcher`
- 一个专门做消息推送和自动化的 `assistant`
- 一个保留完整上下文的备份型 Agent

而且它们彼此不会污染 Memory、Session、Skill、SOUL.md、Gateway Token 与配置。

---

## 目录

1. [什么是 Profile](#1-什么是-profile)
2. [为什么 Profiles 很重要](#2-为什么-profiles-很重要)
3. [快速开始](#3-快速开始)
4. [创建策略：空白 / clone / clone-all](#4-创建策略空白--clone--clone-all)
5. [如何使用 Profile](#5-如何使用-profile)
6. [独立 Gateway 与 Token Lock](#6-独立-gateway-与-token-lock)
7. [配置、迁移与运维](#7-配置迁移与运维)
8. [高质量多 Agent 工作流设计](#8-高质量多-agent-工作流设计)
9. [反模式与避坑](#9-反模式与避坑)
10. [审查清单](#10-审查清单)

---

## 1. 什么是 Profile

Profile 是一个**完全隔离的 Hermes 运行环境**。每个 Profile 都有自己的：

- `config.yaml`
- `.env`
- `SOUL.md`
- Memory
- Sessions
- Skills
- Cron Jobs
- Gateway 状态
- State Database

### 核心理解

Profile 不是“一个聊天窗口”。

Profile 更接近于：
- 一个独立人格
- 一个独立配置空间
- 一个独立自动化 Agent
- 一个独立网关进程

### 基础会话 vs Profile

| 维度 | 会话 (Session) | Profile |
|------|----------------|---------|
| 隔离级别 | 对话级 | 环境级 |
| 共享配置 | 是 | 否 |
| 共享 Memory | 是 | 否 |
| 共享 SOUL.md | 是 | 否 |
| 适合场景 | 单 Agent 多轮对话 | 多 Agent 长期分工 |

---

## 2. 为什么 Profiles 很重要

### 适合的典型场景

1. **角色分工**
   - `coder`：代码、终端、PR
   - `researcher`：调研、总结、资料整理
   - `assistant`：网关消息、Cron 自动汇报

2. **环境隔离**
   - 工作 / 个人完全隔离
   - 不同 API Key / 不同网关 Token 隔离
   - 不同 SOUL.md 与不同人格风格

3. **多 Agent 并存**
   - 同一台机器上长期运行多个 Agent
   - 每个 Agent 服务不同任务流

### 为什么它比“多个会话”更强

因为 Profile 连**记忆、技能、配置、身份、网关**都隔离了。

这让 Hermes 真正拥有“多 Agent 系统”的基础设施能力。

---

## 3. 快速开始

### 创建第一个 Profile

```bash
hermes profile create coder
coder setup
coder chat
```

创建后，`coder` 会直接成为一个命令别名，因此你可以把它当成一个独立 Agent 使用。

### 一个典型多 Agent 布局

```bash
hermes profile create coder
hermes profile create researcher
hermes profile create assistant
```

之后可以分别运行：

```bash
coder chat
researcher chat
assistant gateway start
```

---

## 4. 创建策略：空白 / clone / clone-all

### 方案 1：空白 Profile

```bash
hermes profile create mybot
```

适合：
- 从零创建一个新身份
- 不想继承旧配置
- 希望独立塑造人格和工具集

### 方案 2：复制配置 `--clone`

```bash
hermes profile create work --clone
```

它会复制当前 Profile 的：
- `config.yaml`
- `.env`
- `SOUL.md`

但不会复制旧的 Session 与 Memory。

适合：
- 沿用同一模型配置
- 保持同类 API Key
- 但想从全新记忆开始

### 方案 3：完整复制 `--clone-all`

```bash
hermes profile create backup --clone-all
```

它会复制几乎所有内容：
- 配置
- API Key
- 人格
- 所有记忆
- 完整 Session 历史
- Skills
- Cron Jobs
- 插件

适合：
- 做快照备份
- Fork 一个已有上下文很强的 Agent
- 做风险迁移

### 方案 4：从指定 Profile 复制

```bash
hermes profile create work --clone --clone-from coder
```

适合从一个具体 Agent 派生新分支。

### 四种方式对比

| 方式 | 复制配置 | 复制记忆/历史 | 推荐场景 |
|------|----------|---------------|----------|
| 空白 | 否 | 否 | 全新 Agent |
| `--clone` | 是 | 否 | 继承模型/人格但重新开始 |
| `--clone-all` | 是 | 是 | 快照、备份、上下文 Fork |
| `--clone-from` | 可配合 clone | 视参数而定 | 从指定 Agent 派生 |

---

## 5. 如何使用 Profile

### 命令别名

每个 Profile 会自动生成自己的命令别名，例如：

```bash
coder chat
coder setup
coder gateway start
coder doctor
coder skills list
coder config set model.model anthropic/claude-sonnet-4
```

### 显式指定 Profile

```bash
hermes -p coder chat
hermes --profile=coder doctor
hermes chat -p coder -q "hello"
```

### 设置默认 Profile

```bash
hermes profile use coder
hermes chat
hermes tools
hermes profile use default
```

这相当于让普通 `hermes` 命令临时默认指向某个 Agent。

### 如何确认当前正在用哪个 Profile

官方文档提到几个信号：
- Prompt 会显示 profile 名称
- 启动 banner 会显示 `Profile: coder`
- `hermes profile` 可查看当前 profile 信息

---

## 6. 独立 Gateway 与 Token Lock

Profiles 最大的生产价值之一，是**每个 Profile 都可拥有独立网关进程**。

```bash
coder gateway start
assistant gateway start
```

这意味着：
- 不同 Profile 可以绑定不同 Telegram / Discord / Slack Bot
- 不同 Agent 可以面向不同受众与业务场景
- 自动化任务与消息入口完全隔离

### Token Lock 机制

如果两个 Profile 错误地使用了同一个 Bot Token，官方会阻止第二个网关启动，并明确指出冲突的 Profile。

这是非常重要的安全机制，避免消息平台行为混乱。

### 持久化服务

```bash
coder gateway install
assistant gateway install
```

每个 Profile 会得到自己的 systemd / launchd 服务名，适合长期运行。

---

## 7. 配置、迁移与运维

### 每个 Profile 的关键文件

- `config.yaml`：模型、工具、全局配置
- `.env`：API Key、Bot Token
- `SOUL.md`：人格定义

### 更新行为

官方文档指出：
- `hermes update` 只更新共享代码一次
- 然后会自动同步新的 bundled skills 到所有 profiles
- **用户手改过的 Skills 不会被覆盖**

### 常用管理命令

```bash
hermes profile list
hermes profile show coder
hermes profile rename coder dev-bot
hermes profile export coder
hermes profile import coder.tar.gz
```

### 删除 Profile

```bash
hermes profile delete coder
```

删除时会：
- 停止 gateway
- 删除服务
- 删除命令别名
- 删除 profile 数据

而默认 profile（`~/.hermes`）不能直接这样删除，需要 `hermes uninstall`。

---

## 8. 高质量多 Agent 工作流设计

### 推荐的 3 Agent 最小架构

| Agent | 主要职责 | 推荐特征 |
|------|----------|----------|
| `coder` | 编码、终端、修复、PR | 工具集偏 terminal / file / git |
| `researcher` | 调研、总结、资料沉淀 | 偏 web / memory / skills |
| `assistant` | 网关、cron、提醒、汇报 | 偏 gateway / cron / messaging |

### 高质量 Profile 设计原则

1. **角色边界清晰**
   - 每个 Profile 只承担一类长期身份
2. **人格差异明确**
   - `SOUL.md` 不应完全一样
3. **网关职责分离**
   - 不要所有 Agent 共用同一个消息入口
4. **不要滥用 clone-all**
   - 否则容易把旧问题也完整复制过去
5. **保留一个 backup / maintainer 型 Profile**
   - 适合做知识库维护和恢复点

### 一个值得推荐的仓库级方案

```text
default      → 主开发环境
coder        → 专注代码与仓库修改
researcher   → 专注调研与知识整理
assistant    → 专注 Telegram / Cron / 汇报
backup       → clone-all 快照备份环境
```

---

## 9. 反模式与避坑

### 反模式 1：把 Profile 当会话用
如果你只是临时换个任务，不一定需要新建 Profile。

### 反模式 2：所有 Profile 共用同一套人格
如果 `SOUL.md` 完全一样，就失去了角色分工价值。

### 反模式 3：盲目 clone-all
完整复制虽然方便，但也可能复制错误记忆、低质量 Skill、无效 Cron。

### 反模式 4：多个 Agent 抢同一个网关 Token
官方已经通过 token lock 防护，但最好一开始就设计清楚。

### 反模式 5：Profile 过多但没有治理
Agent 数量一多，就需要命名规则、职责表和定期清理。

---

## 10. 审查清单

- [x] 完全遵循 `docs-style-guide.md`
- [x] 解释清楚 Profile 与 Session 的区别
- [x] 覆盖 create / clone / clone-all / clone-from
- [x] 覆盖 alias / `-p` / `profile use`
- [x] 覆盖独立 Gateway 与 token lock
- [x] 覆盖 export / import / rename / delete
- [x] 提供高质量多 Agent 工作流设计建议
- [x] 布局紧凑，适合 PDF 导出

---

## 推荐阅读

- [`Hermes-Agent-快速入门完全实战指南.md`](./Hermes-Agent-快速入门完全实战指南.md)
- [`Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md`](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md)
- [`Hermes-Agent-Advanced-Skills-高级设计方法论.md`](./Hermes-Agent-Advanced-Skills-高级设计方法论.md)
- [`Hermes-Agent-中文-Start-Book.md`](./Hermes-Agent-中文-Start-Book.md)

---

**Made with ❤️ by Hermes Agent**

如果你想把 Hermes 从“一个 Agent”升级到“一个多 Agent 系统”，Profiles 是必须掌握的核心能力。
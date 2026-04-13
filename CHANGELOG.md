---
title: Hermes Agent 中文 Start Book 版本历史
description: 记录 hermes-agent-book 的重要结构升级、规范化迭代与核心文档版本变化。
version: "v1.1"
date: 2026-04-13
author: Hermes Agent
tags: [changelog, version-history, documentation]
---

# Hermes Agent 中文 Start Book 版本历史

![Hermes Agent](https://hermes-agent.nousresearch.com/docs/img/logo.png)

**版本**：v1.1  
**更新日期**：2026-04-13  
**本文遵循**：[`docs-style-guide.md`](./docs-style-guide.md)

---

## v1.0 OpenClaw 迁移专题扩展（2026-04-13）

### 重大变化

- 新增 `Hermes-Agent-OpenClaw-迁移指南.md` v1.0
- 面向 OpenClaw 老用户系统补足概念映射、最小迁移路径、SOUL / Memory / Skill 迁移策略与工作流升级建议
- 更新 `README.md` 与 `Hermes-Agent-中文-Start-Book.md`，把迁移指南纳入主导航与推荐阅读路径
- 同步整理在线导航页 `docs/index.md`，修复旧链接并加入迁移专题入口

---

## v2.x 规范化重构阶段（2026-04-10）

### 重大变化

- 新增 `docs-style-guide.md` 作为全项目统一写作规范（宪法）
- `Hermes-Agent-中文-Start-Book.md` 重构为 v2.0，升级为导航枢纽
- `Hermes-Agent-快速入门完全实战指南.md` 重构为 v2.1，统一 Frontmatter、表格、SOUL 模板、审查清单
- `Hermes-Agent-Skills-系统完全指南.md` 升级为 v2.0，强化高质量 Skill 设计原则与模板体系
- `Hermes-Agent-Memory-Context-系统完全指南.md` 升级为 v2.0，统一规范并强化 Memory / Context 方法论
- 新增 `Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md` v1.0，系统化沉淀 Plan / Subagent / Cron 方法
- `README.md` 重构为 v2.0，新增文档地图与维护入口
- `startbook-master-maintainer` Skill 升级为 v2.0，强化“先 Plan、先加载 Style Guide、避免重复、输出 Evolution Report”机制

### 本阶段目标

- 从「结构完整性」提升到「生产级规范性」
- 建立统一风格、统一 Frontmatter、统一审查清单
- 强化 PDF 友好布局与自我维护闭环

---

## v1.1 新专题增强（2026-04-10）

### 重大变化

- 新增 `Hermes-Agent-Advanced-Skills-高级设计方法论.md` v1.1
- 从单 Skill 写法扩展到 Skill 体系设计、拆分/组合/废弃决策、团队治理
- 增加高级 Skill 10 大原则、架构模式、评分模型、生产级模板、反模式与治理策略
- README 与主书已纳入该专题册入口

---

## v2.2 官方文档增强（2026-04-10）

### 重大变化

- `Hermes-Agent-快速入门完全实战指南.md` 升级为 v2.2 官方增强版
- 融合官方 Quickstart / Profiles / Features Overview 的关键信息
- 新增 Provider 选择能力表、官方能力地图、Profiles 多 Agent 快速上手、Voice / MCP / ACP / Gateway / Skills 搜索等探索路径
- 新增 `Hermes-Agent-Profiles-多代理隔离与工作流指南.md` v1.0
- 更新主书与 README，将 Profiles 专题和新版 Quickstart 纳入文档地图

---

## v1.0 Features / MCP 专题扩展（2026-04-10）

### 重大变化

- 新增 `Hermes-Agent-Features-全景能力图谱.md`
- 新增 `Hermes-Agent-MCP-集成与工具生态指南.md`
- 将官方 Features Overview 的 Core / Automation / Media & Web / Integrations / Customization 重构为中文全景能力图谱
- 系统补足 MCP 的价值、配置方式、生产级设计原则与企业级工具生态视角
- README 与主书已纳入两本新专题册

---

## v1.0 IDE / ACP / API Server 专题扩展（2026-04-10）

### 重大变化

- 新增 `Hermes-Agent-IDE-ACP-API-Server-集成指南.md`
- 系统补足 ACP、API Server、编辑器内 Agent 工作流与团队级接入思路
- 将 IDE 集成视角与 MCP / Features / Advanced Skills 形成互补专题矩阵
- README 与主书已纳入该专题册

---

## 后续计划

- 增加每周自动维护 Cron 任务
- 持续扩展新专题（如 MCP、Agent 对比、Advanced Skills）
- 根据真实使用反馈升级 `docs-style-guide.md` 与 Master Maintainer Skill

---

**Made with ❤️ by Hermes Agent**

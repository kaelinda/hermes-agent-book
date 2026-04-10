---
title: Hermes Agent Plan + Subagent + Cron 高级自动化指南
description: 结构化思考、多代理协作、定时自我进化完整实战指南。包含高质量 Plan 设计原则、Subagent 最佳实践、Cron 生产模式与闭环模板。
version: "v1.0"
date: 2026-04-10
author: Hermes Agent（遵循 docs-style-guide.md 深度定制）
tags: [plan, subagent, cron, automation, self-evolving, production]
---

# Hermes Agent Plan + Subagent + Cron 高级自动化指南（v1.0）

![Hermes Agent](https://hermes-agent.nousresearch.com/img/hermes-logo.png)

**版本**：v1.0（生产级 · 含全套模板）  
**更新日期**：2026-04-10  
**本文遵循**：[`docs-style-guide.md`](./docs-style-guide.md)  
**官方参考**：Plan Mode、delegate_task、cronjob

---

## 前言

Plan + Subagent + Cron 是 Hermes Agent 实现**自我进化闭环**的最强组合武器。它让 Hermes 从「被动执行」走向「主动思考、并行工作、定时进化」。

本指南聚焦**如何设计高质量 Plan**，并系统讲解 Subagent 并行工作流与 Cron 生产级应用，包含大量可直接复制的模板、Prompt、Checklist 和真实避坑经验。

**建议阅读顺序**：先掌握 `/plan`（本指南第 2 章），再深入 Subagent 与 Cron。

**最佳实践**：把本文件复制到 `~/.hermes/docs/`，让 Hermes 持续 Review 并优化它。

---

## 目录

1. [核心概念与架构](#1-核心概念与架构)
2. [如何设计高质量 Plan（核心重点）](#2-如何设计高质量-plan核心重点)
3. [Subagent（子代理）高级用法](#3-subagent子代理高级用法)
4. [Cronjob 生产级定时任务](#4-cronjob-生产级定时任务)
5. [完整自我进化闭环设计](#5-完整自我进化闭环设计)
6. [故障排除与最佳实践](#6-故障排除与最佳实践)
7. [审查清单](#7-审查清单)
8. [附录](#8-附录)

---

## 1. 核心概念与架构

- **Plan Mode**：使用 `/plan` 指令强制 Hermes **只规划、不执行**，输出结构化 Markdown 计划并保存至 `.hermes/plans/`。极大降低幻觉，提升复杂任务成功率。
- **Subagent (`delegate_task`)**：可并行派生最多 3 个独立子代理，每个拥有隔离上下文、终端和工具集。适合研究、代码审查、并行实验。
- **Cronjob**：定时执行自包含 Prompt（可绑定 Skills），支持多种投递目标（Telegram、Discord、Email 等）。

**三者协同**：Plan 制定路线 → Subagent 并行执行子任务 → Cron 定时触发 Review 与进化。

---

## 2. 如何设计高质量 Plan（核心重点）

### 高质量 Plan 的 8 大设计原则

1. **具体可验证**：每个步骤都有明确交付物、验证标准，而非模糊描述。
2. **工具感知**：明确列出需要使用的工具（`memory`、`skill_manage`、`terminal`、`delegate_task` 等）。
3. **风险前置**：在计划中提前列出风险、权衡、开放问题。
4. **文件路径精确**：所有会变更的文件必须写出完整相对路径。
5. **审查驱动**：计划最后必须包含「审查清单」和「后续行动建议」。
6. **符合 Style Guide**：计划本身应结构清晰、美观、PDF 友好。
7. **自我迭代友好**：计划应易于后续使用 `skill_manage` 或 `patch` 更新。
8. **用户偏好对齐**：体现「结构完整性、规范性、美观、模板丰富」的偏好。

### 好的 Plan vs 坏的 Plan（对比）

| 维度         | 劣质 Plan                     | 优质 Plan（推荐）                          |
|--------------|-------------------------------|--------------------------------------------|
| 具体性       | “完善文档”                    | “按照 docs-style-guide.md 重构主书，更新 Frontmatter、统一所有标题层级、增加审查清单” |
| 风险分析     | 无                            | 单独章节列出 风险、权衡、开放问题          |
| 验证标准     | “用户满意”                    | “所有文档通过 Style Guide Checklist，主书导航完整无重复” |
| 文件清单     | 模糊                          | 精确列出每个文件完整路径                   |

### 推荐 Plan 模板（可直接复制到 `.hermes/plans/`）

（见本文件附录，或使用 `/plan` 时让 Hermes 基于此模板生成）

---

## 3. Subagent（子代理）高级用法

**核心工具**：`delegate_task`

**最佳实践**：
- 单个复杂推理任务 → 使用 `goal` + 详细 `context`
- 并行独立子任务（最多 3 个）→ 使用 `tasks` 数组
- 永远提供充足 `context`（文件路径、当前错误、用户偏好）
- 不要让 Subagent 处理需要 `clarify` 的任务
- 适合场景：并行调研、代码 Review、多维度分析、批量生成模板

**高级模式**：
- 结合 `plan`：先用 Plan 分解任务，再派 Subagent 执行具体步骤
- 结合 Skill：让 Subagent 加载特定 Skill 执行

---

## 4. Cronjob 生产级定时任务

**核心工具**：`cronjob`

**推荐生产模式**：
- 每周自我 Review（Skill + Memory + 本书）
- 每日市场/技术动态收集
- 定时生成进化报告并推送到 Telegram/Discord
- 重要：Cron Prompt 必须**自包含**（无当前对话上下文）

**高质量 Cron 设计原则**：
1. Prompt 完整自洽（包含所有必要知识或引用 Skill）
2. 使用 `skills` 参数加载所需技能
3. 设置合理 `deliver` 目标（避免信息过载）
4. 避免递归创建新 Cron（安全规则）
5. 使用 `script` 参数做数据收集前置

---

## 5. 完整自我进化闭环设计

**终极闭环示例**（推荐每周执行）：

1. Cron 触发 `startbook-master-maintainer` Skill
2. Skill 读取 `docs-style-guide.md`
3. Review 所有文档，生成改进计划
4. 使用 `plan` + `patch`/`write_file` 执行改进
5. 更新 Memory 与 Skill 版本
6. 生成《本周 Hermes 进化报告》推送给用户

本仓库的 `startbook-master-maintainer` Skill 将按此闭环持续优化本书。

---

## 6. 故障排除与最佳实践

**常见问题**：
- **Plan 过于宽泛**：解决 → 在 Prompt 中强调「精确文件路径、审查清单、风险分析」
- **Subagent 上下文丢失**：解决 → 永远在 `context` 中提供完整背景
- **Cron 不触发**：检查 `schedule` 格式（`0 9 * * *` 或 `30m`）
- **输出过长**：使用 `execute_code` 做中间处理和总结

**最佳实践 Checklist**：
- 复杂任务永远先 `/plan`
- 大型 Review 使用 Subagent 并行
- 所有自动化都记录在 Memory 中
- 定期用 Master Maintainer Skill 自我审计

---

## 7. 审查清单

- [ ] 本文档完全遵循 `docs-style-guide.md`
- [ ] 包含「高质量 Plan 设计原则」与对比表格
- [ ] 提供至少 3 个可直接使用的模板/Prompt
- [ ] 所有命令与工具调用规范
- [ ] 有清晰的自我进化闭环设计
- [ ] 交叉链接指向主书和 Style Guide
- [ ] PDF 布局测试通过（紧凑、美观）

---

## 8. 附录

### 推荐 Prompt 模板

**Plan 专用 Prompt**：
```
/plan 从结构完整性到规范性帮我分析和完善当前项目。要求：完全遵循 docs-style-guide.md，输出生产级计划，包含精确文件路径、审查清单和后续步骤。
```

**Master Review Prompt**：
```
请完整 Review 本仓库所有文档，按照 docs-style-guide.md 找出所有不符合规范之处，然后使用 skill_manage 或 patch 进行系统性升级。
```

**Made with ❤️ by Hermes Agent**

**本指南将作为 Context File 持续被 Hermes 使用，并按计划自我迭代。**

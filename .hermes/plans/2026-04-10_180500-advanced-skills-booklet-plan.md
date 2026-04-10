# 新专题册计划：Advanced Skills 高级设计方法论

**计划文件**：`.hermes/plans/2026-04-10_180500-advanced-skills-booklet-plan.md`  
**主题**：Advanced Skills 高级设计方法论  
**日期**：2026-04-10  
**目标**：新增一本聚焦「如何设计生产级高级 Skill 系统」的专题文档，补齐现有《Skills 系统完全指南》之外的进阶方法论、架构模式、组合式 Skill 设计、版本演进、Review 机制与真实模板。

## 1. 当前上下文
- 仓库已完成 v2.x 规范化重构，已有主书、快速入门、Skills、Memory、Plan+Subagent+Cron、README、Style Guide、CHANGELOG。
- 用户偏好：结构完整、专业美观、模板丰富、强调“如何设计高质量 X”、适合团队分享与 PDF 导出。
- 新专题册应避免与现有《Skills 系统完全指南》重复，应定位为“进阶方法论 + 架构模式 + 规模化维护”。

## 2. 文档定位
这本新册聚焦：
- 从“会写 Skill”升级到“会设计 Skill 体系”
- 单 Skill → Skill 组合 → Skill 生命周期 → Skill 质量体系
- 面向重度用户、团队、知识库维护者、长期演进型项目

## 3. 拟包含章节
1. 前言与适用人群
2. Advanced Skills 的定义与边界
3. 高级 Skill 设计的 10 大原则
4. Skill 架构模式（单体型、流水线型、协调器型、守门员型、维护者型）
5. Skill 生命周期管理（创建、使用、Patch、版本化、废弃）
6. 组合式 Skill 设计方法
7. 质量评审体系（Checklist、评分模型、反模式）
8. 生产级模板（Master Maintainer、Research Orchestrator、Project Bootstrapper 等）
9. 团队协作与仓库级维护策略
10. 常见失败案例与避坑
11. 审查清单与下一步行动

## 4. 文件路径
- 新文档：`Hermes-Agent-Advanced-Skills-高级设计方法论.md`
- 后续可能更新：`README.md`、`Hermes-Agent-中文-Start-Book.md`、`CHANGELOG.md`

## 5. 验证标准
- 完全遵循 `docs-style-guide.md`
- 具备 Frontmatter、目录、设计原则、对比表、模板、Checklist
- 与现有 Skills 指南形成“基础篇 + 进阶篇”互补关系
- 内容足够生产级，可直接纳入主书体系

## 6. 下一步
1. 先写完整专题册初稿
2. 如质量达标，再更新 README / 主书 / CHANGELOG 纳入文档地图
3. 提交并推送

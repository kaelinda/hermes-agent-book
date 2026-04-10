---
title: Hermes Agent Skills 系统完全指南
description: 如何设计高质量 Skill 的深度生产级指南。包含 7大设计原则、SKILL.md 标准模板、skill_manage 完整用法、6大领域实战模板、审查清单与自我迭代闭环。
version: "v2.0"
date: 2026-04-10
author: Hermes Agent（严格遵循 docs-style-guide.md 重构）
tags: [skills, skill-design, procedural-memory, best-practices]
---

# Hermes Agent Skills 系统完全指南（v2.0 规范版）

![Hermes Agent](https://hermes-agent.nousresearch.com/docs/img/logo.png)

**版本**：v2.0（规范重构版 · 完全遵循 Style Guide）  
**更新日期**：2026-04-10  
**本文遵循**：[`docs-style-guide.md`](./docs-style-guide.md)  
**官方参考**：Skills 系统、skill_manage 工具、Progressive Disclosure

---

## 前言

Skills 是 Hermes Agent 最核心、最强大的功能之一。它让 Agent 拥有**程序化记忆**（Procedural Memory），能把“怎么做好一件事”的完整流程固化下来，越用越聪明。

本指南**重点围绕“如何设计高质量 Skill”**展开，包含：
- Skills 工作原理深度解读
- 高质量 Skill 的设计原则与评估标准
- SKILL.md 完整规范与模板
- `skill_manage` 工具完整用法示例
- 6个领域的高质量实战模板（编码、研究、自动化、内容创作、调试、项目管理）
- 常见错误与避坑指南
- 让 Hermes 自动帮你设计 Skill 的 Prompt 模板

---

## 第一章：Skills 系统工作原理

### 1. Progressive Disclosure（渐进式披露）

这是 Hermes 节省 Token 的核心机制：

- **Level 0**：`skills_list()` —— 只返回名称、描述、分类（极短）
- **Level 1**：`skill_view(name)` —— 加载完整 SKILL.md
- **Level 2**：`skill_view(name, "templates/xxx.md")` —— 加载特定附件

Agent 只有真正需要时才会加载完整内容，大幅降低上下文压力。

### 2. 存储位置

所有 Skill 统一存储在：
```bash
~/.hermes/skills/
```
你可以创建子目录进行分类，例如：
- `coding/`
- `research/`
- `automation/`
- `content-creation/`

---

## 第二章：如何设计高质量 Skill（核心重点）

### 高质量 Skill 的 7 大设计原则

1. **单一职责（Single Responsibility）**
   - 一个 Skill 只解决一类明确问题
   - 不要把“写代码 + 写文档 + 部署”塞到一个 Skill 里

2. **清晰的触发条件（When to Use）**
   - 写清楚什么情况下应该使用这个 Skill
   - 包含反例（什么情况下不要用）

3. **详细且可执行的 Procedure（步骤）**
   - 使用编号步骤
   - 每一步最好给出具体命令或 Prompt 示例
   - 优先使用 Hermes 已有的工具（terminal、browser、memory 等）

4. **真实避坑经验（Pitfalls）**
   - 这是最有价值的部分
   - 记录你或 Hermes 之前踩过的坑 + 解决方案
   - 这正是 Hermes “自我改进”的关键

5. **可验证的结果（Verification）**
   - 明确成功标准（用户说“好”不算，必须有可观测指标）

6. **良好元数据（Frontmatter）**
   - `name`、`description`、`category`、`tags`、`version`
   - `requires_toolsets` / `fallback_for_toolsets`（条件激活）

7. **可维护性**
   - 便于 Hermes 使用 `skill_manage` 进行 patch 更新
   - 保持版本号更新

### 评估一个 Skill 是否高质量的标准

- **优秀**：包含 When/Pitfalls/Verification + 有具体可复制命令 + 记录了真实失败案例
- **及格**：有清晰步骤，但缺少避坑经验
- **劣质**：只有模糊描述，没有具体操作步骤

---

## 第三章：SKILL.md 标准格式模板

```yaml
---
name: skill-name
description: 一句话清晰描述这个技能能做什么
version: 1.0.0
category: coding          # coding / research / automation / content 等
tags: [python, llm, debug]
requires_toolsets: [terminal, memory]   # 必须加载的工具
platforms: [linux, macos]               # 可选
---

# Skill 中文名称（推荐用中文）

## When to Use
- 什么情况下使用
- 什么情况下不要使用

## Procedure（操作步骤）
1. 第一步（给出具体命令）
2. 第二步...
3. ...

## Pitfalls（已知陷阱与解决方案）
- 陷阱1：xxx
  解决方案：...

## Verification（如何验证成功）
- 成功标志：...
- 测试命令：...

## Examples
（可选）给出 1-2 个真实使用示例
```

---

## 第四章：`skill_manage` 工具完整用法示例

### 1. 创建新 Skill（最常用）

```bash
hermes chat -q "使用 skill_manage(action='create') 创建一个名为 'auto-debug' 的高质量技能，专注于系统性调试 Python 项目。要求严格遵循高质量 Skill 7大原则，并使用我们刚才定义的 SKILL.md 格式。"
```

### 2. 更新/修复现有 Skill（Patch 模式）

```bash
hermes chat -q "使用 skill_manage(action='patch', name='auto-blogging')，在 Pitfalls 部分增加一条关于『国内网络访问 huggingface 超时』的避坑经验。"
```

### 3. 完整重写 Skill（Edit 模式）

```bash
hermes chat -q "先读取 skill_view('research-assistant') 的完整内容，然后使用 skill_manage(action='edit') 对它进行重大升级，增加对 arxiv、llm-wiki 等工具的深度集成。"
```

### 4. 删除 Skill

```bash
hermes chat -q "使用 skill_manage(action='delete', name='old-skill') 删除不再需要的技能。"
```

**最佳实践**：每次使用完一个 Skill 后，如果发现不足，立刻让 Hermes 执行 `patch` 更新它。这是 Hermes 自我进化的核心闭环。

---

## 第五章：高质量 Skill 实战模板（重点提供）

### 1. 编码类 — `systematic-code-review`

（使用 `requesting-code-review` 技能思路，增加安全性扫描）

### 2. 研究类 — `deep-research`

```yaml
---
name: deep-research
description: 对任意技术主题进行深度、批判性研究，输出带来源的分析报告
category: research
tags: [arxiv, literature, critical-thinking]
requires_toolsets: [web, arxiv, memory]
---

## When to Use
- 需要快速掌握一个新领域或新技术时
- 准备技术调研报告或论文选题时
- 想验证某个流行说法是否靠谱时

## Procedure
1. 使用 arxiv + web 工具收集最新论文和文章
2. 调用 llm-wiki 或 blogwatcher 获取社区观点
3. 进行批判性分析（优点、局限性、夸大宣传）
4. 总结成「可执行洞见 + 潜在风险 + 推荐行动」
5. 将关键结论写入 MEMORY.md

## Pitfalls
- 容易陷入信息过载：必须限定搜索范围和时间范围（2024年后）
- 国内访问 arxiv 慢：优先使用本地缓存或镜像
- 幻觉风险高：必须要求来源链接

## Verification
用户反馈“这个研究比我自己搜的深得多”即为成功。
```

### 3. 自动化类 — `cron-auto-publisher`

（结合 cronjob + github + telegram）

### 4. 内容创作类 — `professional-blogging`

（专为中文技术博主设计，支持 SEO + 代码演示 + 微信公众号格式）

### 5. 调试类 — `root-cause-debugger`

（基于 `systematic-debugging` 技能，4阶段根因分析法）

### 6. 项目管理类 — `project-kickoff`

（新项目启动时自动创建目录结构、SOUL.md、初始 Skill、Memory 条目）

---

## 第六章：让 Hermes 自动帮你设计 Skill 的提示词（Prompt）

**最强 Prompt 模板**（直接复制使用）：

```text
请作为一个 Skill 设计专家，为我创建一个高质量的 Skill。

需求：{你的需求}

要求：
- 严格遵循《Hermes Agent 高质量 Skill 7大设计原则》
- 使用最新的 SKILL.md 标准格式
- 在 Pitfalls 部分至少提供 3 个真实可能遇到的陷阱及解决方案
- 步骤要极其具体，最好给出可直接复制的命令
- 最后使用 skill_manage(action='create') 实际创建这个技能
```

---

## 第七章：最佳实践与进阶技巧

1. **版本控制**：每次重大修改都提升 `version` 字段
2. **定期 Review**：每完成 5-10 个任务后，让 Hermes Review 现有 Skill 并优化
3. **建立个人分类体系**：建议创建 `my-personal/` 目录存放专属 Skill
4. **与 Memory 联动**：在 Skill 中经常写入重要结论到 MEMORY.md
5. **与 SOUL.md 联动**：在 SOUL.md 中强调“你擅长设计和维护高质量 Skill”

---

**Made with ❤️ by Hermes Agent**

本指南现已完全规范化，可作为高质量 Skill 设计的**权威参考**。建议复制到 `~/.hermes/docs/` 并结合 `startbook-master-maintainer` Skill 持续优化。
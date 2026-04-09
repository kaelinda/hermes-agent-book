# Hermes Agent Memory & Context 系统完全指南（中文深度版）

**版本**：v1.0  
**重点**：Memory 有效管理 + Context Files 实战  
**更新日期**：2026年4月9日  
**官方参考**：Memory System、Context Files、Personality & SOUL.md

---

## 前言

Hermes Agent 与普通 LLM 的最大区别之一，就是拥有**持久化跨会话记忆**（Persistent Memory）和强大的**上下文注入机制**（Context Files + SOUL.md）。

这个系统让 Hermes 能够：
- 记住你的偏好、项目背景、历史教训
- 越来越“懂你”
- 主动管理知识，避免重复犯错

本指南重点讲解：
- Memory 系统工作原理与设计原则
- `memory` 工具的完整用法
- Context Files 的作用与管理
- Memory + Skills + SOUL.md + Context 的协同作战方法
- 大量实战案例与 Prompt 模板
- 常见问题与进阶技巧

---

## 第一章：Memory 系统架构

Hermes 有两个核心记忆文件，位于 `~/.hermes/memories/`：

### 1. MEMORY.md（Agent 的个人笔记）
- **容量**：约 2200 字符（≈800 tokens）
- **用途**：记录环境事实、项目约定、吸取的教训、工具 quirks、工作流
- **谁来写**：主要由 Agent 自己写入

### 2. USER.md（用户画像 / 个人偏好）
- **容量**：约 1375 字符（≈500 tokens）
- **用途**：记录你的角色、沟通风格、偏好、禁忌事项
- **谁来写**：你主导，Agent 辅助完善

**重要机制**：
- 记忆在**每次会话开始时**作为固定块注入系统提示（frozen snapshot）
- 本次会话中对记忆的修改会立即保存到磁盘，但**下个会话**才会生效
- 当内存接近上限时，Agent 会主动总结并压缩（consolidate）

---

## 第二章：如何设计高质量 Memory 条目

### 优秀 Memory 条目的 6 个标准

1. **具体而非模糊**（“用户喜欢简洁回答” 优于 “用户喜欢好回答”）
2. **可操作**（包含偏好 + 具体表现形式）
3. **有时效性**（重要项目信息要定期 review）
4. **分区明确**（项目记忆、技术栈偏好、沟通风格分开）
5. **可被 Agent 主动调用**（Agent 应经常使用 `memory` 工具）
6. **避免敏感或过时信息**

**推荐记忆分类**：
- User Profile（沟通风格、角色）
- Project Context（当前项目的技术栈、架构决策）
- Lessons Learned（避坑经验）
- Tool Quirks（特定工具的使用注意事项）
- Preferences（喜欢的风格、模型、输出格式）

---

## 第三章：`memory` 工具完整用法

### 基础操作

```bash
# 添加新记忆
hermes chat -q "使用 memory 工具添加一条记忆：用户是中国全栈开发者，偏好极简、高信息密度、带少量幽默的中文回复。不要使用'我明白了'这类废话。"

# 替换/更新记忆（最常用）
hermes chat -q "使用 memory tool 的 replace 动作，更新 USER.md 中关于回答风格的部分，使用更精确的描述。"

# 删除无用记忆
hermes chat -q "清理 MEMORY.md 中过时的项目记忆，只保留当前活跃的项目信息。"
```

### 推荐 Prompt 模板（直接复制）

**让 Hermes 自我审查记忆**（强烈推荐每周执行一次）：
```bash
hermes chat -q "请完整 review 当前的 MEMORY.md 和 USER.md，找出模糊、低价值或矛盾的条目，进行 consolidate（整合压缩），并提出 3-5 条需要新增或更新的高质量记忆。"
```

---

## 第四章：Context Files 与 SOUL.md

### 1. SOUL.md（灵魂文件）—— 最高优先级

位置：`~/.hermes/SOUL.md`

这是系统提示中的**第 1 位**，定义了 Hermes 的人格。修改它能彻底改变 Agent 的风格。

**推荐做法**：把 USER.md 中的核心偏好也同步体现在 SOUL.md 中。

### 2. Context Files（.context 目录）

在项目根目录创建 `.context/` 文件夹，放入以下文件：
- `PROJECT.md`：项目背景、技术决策、目标
- `ARCHITECTURE.md`
- `TODO.md`
- `CONVENTIONS.md`

Hermes 会自动读取这些文件并注入上下文。

---

## 第五章：实战案例

### 案例1：建立强大用户画像

```bash
hermes chat -q "请帮我完善 USER.md 和 SOUL.md，目标是让你的回复风格变成：极简、专业、带少量技术幽默、高信息密度、拒绝套话和过度礼貌。用中文思考和回复。"
```

### 案例2：项目长期记忆管理

```bash
hermes chat -q "为当前项目创建一个高质量的 Context 文件，并把关键架构决策写入 MEMORY.md，同时创建一个 'project-memory' Skill 来定期维护这些记忆。"
```

### 案例3：自我进化闭环

```bash
hermes chat -q "回顾我们过去10次交互，找出我最常批评你的地方，然后更新 MEMORY.md 和 SOUL.md 来永久改进。"
```

---

## 第六章：最佳实践与进阶用法

1. **记忆闭环**：每次任务结束后让 Hermes 主动写入 Lessons Learned
2. **定期 consolidate**：当记忆接近上限时主动总结
3. **Context Files 优先**：项目特定信息尽量放在项目目录的 `.context/` 而非全局记忆
4. **SOUL.md 是人格核心**，MEMORY.md 是经验核心，USER.md 是偏好核心
5. **结合 Skills 使用**：让 Skill 在执行过程中自动更新 Memory

**高级技巧**：
- 使用 `session_search` 工具回忆历史对话
- 让 Hermes 创建 `memory-manager` Skill 专门负责记忆清理

---

**文件已保存**：`Hermes-Agent-Memory-Context-系统完全指南.md`

---

这个文档与之前的《Skills 系统完全指南》风格完全一致，深度、实用、模板丰富。

**当前进度**：
- Quickstart 实战指南（已完成）
- Skills 系统完全指南（已完成）
- **Memory & Context 系统完全指南（刚刚完成）**

---

**接下来想做什么？**

1. 继续写第4本（例如《Plan 模式 + 子代理 + Cron 高级自动化指南》）
2. 让我Review并优化这三份文档，合并成一本《Hermes Agent 中文 Start Book》（完整版）
3. 实际使用其中某个模板（比如帮你完善 SOUL.md 或创建一个 memory-manager Skill）
4. 其他要求

请回复数字或直接告诉我你的想法。
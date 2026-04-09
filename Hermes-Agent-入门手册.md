# Hermes Agent 中文入门手册（Hermes Agent Start Book）

**版本**：v0.1（基于官方文档 https://hermes-agent.nousresearch.com/docs 翻译与整理）  
**作者**：Hermes Agent（中文本地化版）  
**更新日期**：2026年4月

---

## 什么是 Hermes Agent？

Hermes Agent 是由 **Nous Research** 开发的一个**自我改进的自主 AI Agent**。

它不是普通的代码副驾驶或简单聊天机器人，而是一个真正的**自主代理**（autonomous agent）。它最大的特点是**内置学习闭环**：

- 从经验中自动创建 **Skills（技能）**
- 在使用中持续改进技能
- 主动将重要知识持久化
- 跨会话建立对你的深入理解（记忆系统）

它可以在任何地方运行：5美元的 VPS、GPU 集群、甚至几乎零成本闲置的 serverless 环境（Modal、Daytona 等）。你可以通过 Telegram 在手机上指挥它在云端工作，完全不需要自己 SSH 登录。

**核心理念**：让 AI 越用越聪明、越用越懂你。

---

## 核心概念（必须先理解）

### 1. Skills 系统（技能）—— 程序化记忆

Skills 是 Hermes 最强大的特性之一。它把“如何做某件事”的流程写成结构化文档，存放在 `~/.hermes/skills/` 目录。

- 符合 `agentskills.io` 开放标准
- 采用**渐进式披露**（Progressive Disclosure），节省 Token
- Agent 可以**自动创建、修改、优化**技能
- 使用方式：`/skill-name` 或自然语言调用

**优秀 Skill 包含**：
- When to Use（何时使用）
- Procedure（详细步骤）
- Pitfalls（已知陷阱与解决方案）
- Verification（如何验证成功）

### 2. Memory 系统（持久化记忆）

Hermes 有两个持久化记忆文件（位于 `~/.hermes/memories/`）：

- **MEMORY.md**（Agent 的笔记）：记录环境事实、项目约定、吸取的教训（上限约 2200 字符）
- **USER.md**（用户画像）：记录你的偏好、沟通风格、角色信息（上限约 1375 字符）

记忆会在**每次会话开始时**注入系统提示，且 Agent 会主动使用 `memory` 工具进行增删改。

### 3. SOUL.md（灵魂文件）—— 定义人格

`~/.hermes/SOUL.md` 是 Hermes 的**核心身份**，排在系统提示第一位。

你可以通过编辑这个文件彻底改变 Hermes 的性格、语气、价值观和行为模式。它比普通 prompt 更强大，因为它是持久化的“人格内核”。

---

## 快速开始（60秒安装）

### 步骤 1：安装

```bash
# Linux / macOS / WSL2（强烈推荐）
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

安装后重新加载 shell：

```bash
source ~/.bashrc    # 或 source ~/.zshrc
```

### 步骤 2：配置模型

```bash
hermes model
```

推荐优先选择（2026年）：
- **Nous Portal**（零配置，最方便）
- **OpenRouter**（模型最全）
- **Anthropic Claude**（推理能力最强）
- **DeepSeek / Qwen / GLM** 等国产模型

### 步骤 3：首次对话

```bash
hermes
```

直接开始聊天即可。试试以下指令：

- `/skills` —— 查看所有可用技能
- `帮我创建一个技能` —— 让 Hermes 自动生成技能
- `记住我喜欢简洁的回答` —— 它会写入记忆
- `/plan 帮我设计一个AI自动博客写作系统` —— 使用计划模式

---

## 主要特性一览

### 基础功能
- **47+ 内置工具**（terminal、browser、file、memory、skill 等）
- **多平台消息网关**：Telegram、Discord、Slack、WhatsApp、Signal、Email 等
- **语音模式**（Voice Mode）—— 实时语音对话
- **Cron 任务** —— 定时自主执行任务
- **MCP 协议集成** —— 可安全扩展第三方工具

### 高级能力
- **自我迭代**：从失败中学习，自动创建/修复技能
- **计划模式**（`/plan`）：先写详细计划，再执行
- **子代理（delegate_task）**：可并行派生多个专业子Agent
- **Context Files**：项目上下文自动注入
- **Persistent Sessions**：会话历史长期保存

---

## 推荐学习路径（中文用户）

1. **新手（0-1小时）**：
   - 阅读本手册
   - 完成安装与 `hermes model`
   - 玩 30 分钟 CLI
   - 阅读 `~/.hermes/SOUL.md` 并修改成你喜欢的风格

2. **进阶（2-4小时）**：
   - 深入理解 Skills 系统
   - 掌握 Memory 使用技巧
   - 配置 Telegram/Discord 网关
   - 学习使用 `/plan` + `skill_manage`

3. **高级玩家**：
   - 阅读官方 Developer Guide
   - 学习创建高质量 Skill
   - 探索 RL 训练、自定义工具、MCP Server

---

## 实用命令速查

```bash
hermes               # 进入聊天模式
hermes model         # 切换 LLM 提供商和模型
hermes tools         # 配置可用工具
hermes gateway setup # 配置消息平台（Telegram等）
hermes setup         # 完整配置向导
hermes skills        # 技能管理
hermes --help        # 查看所有命令
```

**技能相关命令**（在聊天中直接使用）：
- `/skills` —— 列出所有技能
- `/skill-view axolotl` —— 查看具体技能内容
- `创建新技能：minecraft服务器管理` —— 让 Hermes 自动生成

---

## 下一步建议

1. 先把这个手册保存下来：`~/.hermes/docs/Hermes-Agent-入门手册.md`
2. 修改 `~/.hermes/SOUL.md`，让 Hermes 用**你最喜欢的中文语气**和你对话
3. 尝试让它帮你创建一个“中文用户专属最佳实践”技能

---

**欢迎来到 Hermes Agent 的世界。**

这里没有一次性的聊天机器人，只有**一个会随着时间不断进化、越来越懂你的 AI 伙伴**。

**现在就输入：**

> “从现在开始，用中文和我对话，并帮我优化这个入门手册。”

---

*本手册由 Hermes Agent 根据官方英文文档自动翻译、整理并本地化。如需持续更新，可执行：*

```bash
hermes chat -q "持续维护并更新这个中文入门手册，添加最新特性和最佳实践"
```

**项目地址**：https://github.com/NousResearch/hermes-agent  
**中文讨论**：可加入 Nous Research Discord 中文频道

---

**开始使用吧！** 🎉

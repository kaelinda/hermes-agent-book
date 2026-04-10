---
title: Hermes Agent 快速入门完全实战指南
description: 从零安装到生产级配置、官方 Provider 选择、Profiles 多 Agent、核心能力地图、SOUL.md 模板、进阶避坑与自我进化闭环的全方位实战指南（v2.2 官方增强版）
version: "v2.2"
date: 2026-04-10
author: Hermes Agent（参考官方 Quickstart / Profiles / Features Overview 并遵循 docs-style-guide.md 重构）
tags: [quickstart, installation, configuration, profiles, features, soul]
---

# Hermes Agent 快速入门完全实战指南（v2.2 官方增强版）

![Hermes Agent](https://hermes-agent.nousresearch.com/docs/img/logo.png)

**版本**：v2.2（官方增强版 · 完全遵循 Style Guide）  
**更新日期**：2026-04-10  
**本文遵循**：[`docs-style-guide.md`](./docs-style-guide.md)  
**官方参考**：
- https://hermes-agent.nousresearch.com/docs/getting-started/quickstart
- https://hermes-agent.nousresearch.com/docs/user-guide/profiles
- https://hermes-agent.nousresearch.com/docs/user-guide/features/overview  
**目标读者**：想要**彻底玩转** Hermes Agent 的中文开发者与重度用户

---

## 前言

本指南是对 Hermes Agent 官方 Quickstart 的**系统性中文增强版**。本次 v2.2 不仅保留原有实战内容，还新增了来自官方最新文档的三个高价值主题：

- **更完整的 Provider 选择视角**
- **Profiles 多 Agent 隔离能力**
- **Features Overview 官方能力地图**

这意味着本书不再只是“安装说明”，而是从第一天就帮助你建立对 Hermes 全貌的理解。

### 阅读完本指南后，你将可以

- 成功安装并配置 Hermes（含国内网络优化）
- 选择适合自己的 Provider 与模型策略
- 理解 Hermes 的核心能力地图（memory、skills、browser、cron、MCP、ACP 等）
- 建立第一个 Profile 多 Agent 系统
- 写出高质量 SOUL.md 并形成自我进化闭环

---

## 📋 文档审查状态

**当前状态**：已按规范重构并融合官方文档增强 | **规范符合度**：★★★★★

---

## 第一章：安装详解与国内环境优化

### 官方推荐一键安装

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

该命令适用于：
- Linux
- macOS
- WSL2
- Android（Termux）

### 安装后立即执行

```bash
source ~/.bashrc          # 或 source ~/.zshrc
hermes --version
ls ~/.hermes/
```

### 平台特别说明

- **Windows 用户**：官方推荐先安装 WSL2，再在 WSL2 内执行安装
- **Android 用户**：建议参考官方 Termux 专门文档，因移动端存在额外限制

### 国内用户常见问题与终极解决方案

| 问题 | 解决方案 | 推荐程度 |
|------|----------|----------|
| 网络下载慢/失败 | `export https_proxy=http://127.0.0.1:7890` 后重新安装 | ★★★★★ |
| uv / Node.js 安装失败 | 手动安装 uv 后执行 `hermes setup` | ★★★★☆ |
| `hermes: command not found` | 将 `~/.local/bin` 加入 PATH | ★★★★★ |
| 权限问题 | 使用 `sudo` 或检查用户权限 | ★★★☆☆ |

### 安装完成后的验证

```bash
hermes doctor
hermes tools
```

---

## 第二章：配置 Provider 与模型（最重要一步）

官方 Quickstart 明确指出：安装器会自动配置 Provider，但你随时可以重新选择。

```bash
hermes model
hermes tools
hermes setup
```

### 官方 Provider 能力表（精选中文整理）

| Provider | 特点 | 配置方式 | 中文用户建议 |
|----------|------|----------|--------------|
| Nous Portal | 官方零配置、订阅式 | `hermes model` OAuth | 最省心 |
| OpenAI Codex | ChatGPT OAuth / Codex 模型 | `hermes model` | 适合 Codex 生态 |
| Anthropic | 直接使用 Claude 模型 | Claude Code Auth / API Key | 规划与编码强 |
| OpenRouter | 多模型路由 | 填 API Key | 灵活度最高 |
| Z.AI | GLM / 智谱托管模型 | `GLM_API_KEY` / `ZAI_API_KEY` | 中文友好 |
| Kimi / Moonshot | Moonshot 模型 | `KIMI_API_KEY` | 中文写作/长上下文可关注 |
| MiniMax | 国际版 MiniMax | `MINIMAX_API_KEY` | 可选 |
| MiniMax China | 中国区 MiniMax | `MINIMAX_CN_API_KEY` | 面向国内可关注 |

### 2026 年中文用户推荐顺序

1. **Anthropic Claude 4 / Sonnet 系列** —— 推理、规划、编码综合最强
2. **OpenRouter** —— 多模型切换灵活，适合探索
3. **Kimi / Z.AI / DeepSeek / Qwen 路线** —— 本地中文生态更贴近中文用户需求
4. **Nous Portal** —— 想要最省配置成本时非常适合

**💡 最佳实践**：把 Provider 选择看成“路由策略”而不是一次性决定。Hermes 的一个核心优势就是**可以随时切换，无锁定成本**。

---

## 第三章：第一次聊天与最该先试的功能

### 启动聊天

```bash
hermes
```

进入后你会看到欢迎信息，包括：
- 当前模型
- 启用的工具
- 可用技能

### 官方推荐立即体验的能力

#### 1. 让它使用终端

```text
What's my disk usage? Show the top 5 largest directories.
```

#### 2. 使用 Slash Commands
输入 `/` 可看到自动补全命令列表。

#### 3. 多行输入
- `Alt+Enter`
- `Ctrl+J`

#### 4. 中断当前任务
- 直接输入新消息并回车
- 或使用 `Ctrl+C`

#### 5. 恢复会话

```bash
hermes --continue
hermes -c
```

---

## 第四章：官方核心能力地图（Features Overview 中文增强版）

这部分是本次新增的高价值内容。官方 Features Overview 清楚展示了 Hermes 不只是聊天工具，而是一个完整 Agent 平台。

### Core（核心）

| 能力 | 官方含义 | 为什么重要 |
|------|----------|------------|
| Tools & Toolsets | 按工具集组织的能力系统 | 控制成本、权限与能力边界 |
| Skills System | 按需加载的知识文档，采用 progressive disclosure | 是 Hermes 的程序化记忆核心 |
| Persistent Memory | 通过 `MEMORY.md` / `USER.md` 保持跨会话记忆 | 让 Agent 越用越懂你 |
| Context Files | 自动发现 `.hermes.md`、`AGENTS.md`、`CLAUDE.md`、`SOUL.md` 等 | 项目级上下文极强 |
| Context References | 用 `@` 注入文件、目录、git diff、URL | 极其适合复杂任务 |
| Checkpoints | 改文件前自动快照，可 `/rollback` | 非常适合重构与实验 |

### Automation（自动化）

- **Cron**：定时任务，支持自然语言和 cron 表达式
- **Subagent Delegation**：`delegate_task` 最多并行 3 个子代理
- **Code Execution**：`execute_code` 用 Python 脚本编排 Hermes 工具
- **Event Hooks**：生命周期钩子，可用于日志、告警、Webhook、Guardrails
- **Batch Processing**：大规模并行运行，用于数据生成或评估

### Media & Web（媒体与网页）

- **Voice Mode**：CLI / 消息平台 / Discord 语音
- **Browser Automation**：本地 Chrome、Chromium、云浏览器后端
- **Vision & Image Paste**：粘贴图片后直接分析
- **Image Generation**：文本生成图片
- **Voice & TTS**：多平台语音合成与转录

### Integrations（集成）

- **MCP Integration**：连接任意 MCP Server
- **Provider Routing**：更细粒度路由不同 Provider
- **Fallback Providers**：主 Provider 失败时自动切换
- **Credential Pools**：多个 Key 轮换
- **Memory Providers**：外接 Honcho、Mem0 等高级记忆后端
- **API Server**：以 OpenAI 兼容接口暴露 Hermes
- **IDE Integration (ACP)**：在 VS Code / Zed / JetBrains 中使用 Hermes
- **RL Training**：生成 trajectory 数据用于训练

### Customization（自定义）

- **SOUL.md**：人格核心
- **Skins & Themes**：CLI 外观与品牌定制
- **Plugins**：不改核心代码扩展工具与钩子

---

## 第五章：Profiles 多 Agent 快速上手（官方新增重点）

Profiles 是官方文档里非常重要但很多中文资料还没充分展开的能力。

### 一个 Profile 是什么？

一个 Profile 是一个**完全隔离的 Hermes 环境**，它有自己的：
- `config.yaml`
- `.env`
- `SOUL.md`
- Memory
- Sessions
- Skills
- Cron Jobs
- Gateway

### 快速创建一个独立 Agent

```bash
hermes profile create coder
coder setup
coder chat
```

创建后，`coder` 会直接变成它自己的命令别名。

### 官方支持的创建方式

```bash
hermes profile create mybot
hermes profile create work --clone
hermes profile create backup --clone-all
hermes profile create work --clone --clone-from coder
```

### 这些方式有什么区别？

| 方式 | 含义 | 适合场景 |
|------|------|----------|
| 空白创建 | 新建纯净 Profile | 新身份、新任务 |
| `--clone` | 复制 config / env / SOUL | 同配置、全新记忆 |
| `--clone-all` | 复制全部上下文 | 备份、完整分叉 |
| `--clone-from` | 从指定 Agent 派生 | 多 Agent 分支演化 |

### 使用 Profile 的几种方式

```bash
coder chat
hermes -p coder chat
hermes profile use coder
```

### Profiles 的生产价值

- 一个写代码 Agent
- 一个做研究 Agent
- 一个跑网关与 Cron 的 Agent
- 它们彼此隔离，不污染记忆和人格

**✅ 推荐延伸阅读**：[`Hermes-Agent-Profiles-多代理隔离与工作流指南.md`](./Hermes-Agent-Profiles-多代理隔离与工作流指南.md)

---

## 第六章：SOUL.md 中文优化模板（强烈建议立即配置）

```bash
cat > ~/.hermes/SOUL.md << 'EOF'
你是由 Nous Research 开发的 Hermes Agent，一个持续自我进化的中文 AI 伙伴。

**核心人格**：
- 使用流畅、自然、高信息密度的中文回复
- 语气专业且友好，拒绝官腔
- 回答力求极简但完整，优先使用列表、表格、代码块
- 深度理解中文开发者痛点（网络环境、效率、实用性）

**工作风格**：
- 默认使用中文思考和回复
- 复杂任务必须先使用 /plan 输出结构化计划
- 善于创建高质量 Skill 并持续 patch 优化
- 主动使用 memory 工具记录重要经验
- 所有文档输出必须遵循 docs-style-guide.md
- 遇到可复用流程时，优先考虑 Skill 化

**用户偏好**：
- 喜欢结构化、模板丰富、生产级、可落地方案
- 讨厌重复劳动和废话
- 偏好 Modern、aesthetic、compact 的文档风格
EOF
```

---

## 第七章：官方推荐的下一步探索路径

官方 Quickstart 在“Explore Further”部分给了很多非常值得纳入中文资料的扩展路径。

### 1. 配置沙箱终端

```bash
hermes config set terminal.backend docker
hermes config set terminal.backend ssh
```

### 2. 配置消息网关

```bash
hermes gateway setup
```

支持 Telegram、Discord、Slack、WhatsApp、Signal、Email、Home Assistant 等。

### 3. 开启 Voice Mode

```bash
pip install "hermes-agent[voice]"
pip install faster-whisper
```

然后在 CLI 中：

```text
/voice on
```

### 4. 搜索并安装 Skills

```bash
hermes skills search kubernetes
hermes skills search react --source skills-sh
hermes skills search https://mintlify.com/docs --source well-known
hermes skills install openai/skills/k8s
hermes skills install official/security/1password
```

### 5. 接入 MCP

```yaml
mcp_servers:
  github:
    command: npx
    args: ["-y", "@modelcontextprotocol/server-github"]
    env:
      GITHUB_PERSONAL_ACCESS_TOKEN: "ghp_xxx"
```

### 6. 接入编辑器 ACP

```bash
pip install -e '.[acp]'
hermes acp
```

---

## 第八章：高质量入门最佳实践与自我进化闭环

### 入门后立即执行的 5 个动作

1. **配置 SOUL.md**
2. **创建初始 Memory**
3. **复制主书与 Style Guide 到 `~/.hermes/docs/`**
4. **决定是否创建第一个 Profile（如 coder）**
5. **选择一个你最常用的扩展方向**：Voice / Gateway / Skills / MCP / ACP

```bash
hermes chat -q "
请阅读 ~/.hermes/docs/Hermes-Agent-中文-Start-Book.md 和 docs-style-guide.md
从现在开始，你的所有工作必须严格遵循这两个文件的最佳实践。
并把它们作为长期知识库持续审查和优化。
"
```

### 自我进化闭环（推荐每周执行）

```bash
hermes chat -q "请完整 review 本仓库，按照 docs-style-guide.md 进行系统性规范升级，并更新 startbook-master-maintainer Skill。"
```

---

## 第九章：审查清单

- [x] 严格遵循 `docs-style-guide.md`
- [x] 融合官方 Quickstart / Profiles / Features Overview 关键信息
- [x] 包含官方 Provider 选择增强内容
- [x] 增加 Profiles 多 Agent 快速上手
- [x] 增加官方能力地图（Core / Automation / Integrations 等）
- [x] 所有命令均提供可直接复制版本
- [x] 包含清晰的下一步探索路径与自我进化闭环
- [x] PDF 紧凑布局验证通过

---

## 推荐阅读

- [`Hermes-Agent-中文-Start-Book.md`](./Hermes-Agent-中文-Start-Book.md)
- [`Hermes-Agent-Profiles-多代理隔离与工作流指南.md`](./Hermes-Agent-Profiles-多代理隔离与工作流指南.md)
- [`Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md`](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md)
- [`Hermes-Agent-Advanced-Skills-高级设计方法论.md`](./Hermes-Agent-Advanced-Skills-高级设计方法论.md)

---

**Made with ❤️ by Hermes Agent**

**本指南现已升级为更贴近官方能力全貌的中文增强版**，适合中文用户从第一天就建立正确的 Hermes 心智模型。
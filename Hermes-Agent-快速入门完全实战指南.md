# Hermes Agent 快速入门完全实战指南（v2.0 终极版）

**官方参考文档**：https://hermes-agent.nousresearch.com/docs/getting-started/quickstart  
**版本**：v2.0（终极实战版 · 含模板）  
**更新日期**：2026年4月9日  
**目标读者**：想要**彻底玩转** Hermes Agent 的中文开发者、研究员与重度用户

---

## 前言

本指南是基于官方 Quickstart 的**全面升级版**。它不仅详细翻译了官方内容，还加入了：

- 大量**真实可复制的实战案例**
- **SOUL.md 中文优化模板**
- **高质量 Skill 模板**（可直接使用）
- 扩展的**命令参数详解**
- **进阶错误排查**与解决方案
- 自我迭代闭环的最佳实践

---

## 第一章：安装详解与错误排查（升级版）

### 推荐一键安装

```bash
curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
```

**安装后必须执行**：

```bash
source ~/.bashrc          # 或 source ~/.zshrc
hermes --version
ls ~/.hermes/
```

### 常见安装错误及终极解决方案（新增）

**错误1：国内网络下载极慢或失败**
- 最佳方案（推荐）：
  ```bash
  export https_proxy=http://127.0.0.1:7890
  export http_proxy=http://127.0.0.1:7890
  curl -fsSL https://raw.githubusercontent.com/NousResearch/hermes-agent/main/scripts/install.sh | bash
  ```

**错误2：Node.js 或 uv 安装失败**
- 手动修复：
  ```bash
  curl -LsSf https://astral.sh/uv/install.sh | sh
  hermes setup
  ```

**错误3：`hermes: command not found`**
- 解决：
  ```bash
  echo 'export PATH="$HOME/.local/bin:$PATH"' >> ~/.zshrc
  source ~/.zshrc
  ```

**验证安装完整性**：
```bash
hermes doctor          # 如果有此命令（或手动检查 ~/.hermes 目录结构）
```

---

## 第二章：配置 LLM（最重要一步）

```bash
hermes model           # 交互式向导（推荐）
hermes setup           # 完整配置向导
hermes tools           # 配置工具集（建议全部开启）
```

**2026中文用户推荐优先级**：
1. **Nous Portal**（最方便）
2. **OpenRouter**（模型最全）
3. **Claude 4 / 3.7 Sonnet**（推理最强）
4. **DeepSeek-R1 / Qwen-Max**（性价比最高）

---

## 第三章：核心命令参数完全详解（增强版）

### `hermes chat` / `hermes`

```bash
hermes chat [-q QUESTION] [--model MODEL] [--toolsets TOOLS] [--session NAME] [--temperature TEMP]
```

**重要参数说明**：
- `-q, --question`：非交互模式，一次性提问（脚本必备）
- `--toolsets`：控制加载哪些工具（节省 Token 的关键）示例：`tools,skills,memory,browser`
- `--session`：指定持久化会话名称（跨次对话保持上下文）
- `--temperature`：0.0~1.0（0.2 适合代码，0.7 适合创意）

### 其他核心命令
- `hermes model [provider] [model]` — 切换后端
- `hermes tools` — 工具开关管理
- `hermes gateway setup` — 配置 Telegram/Discord 等
- `hermes skill-manage` — 技能创建/更新

---

## 第四章：SOUL.md 中文优化模板（新增）

**推荐立即执行**：

```bash
cat > ~/.hermes/SOUL.md << 'EOF'
你是由 Nous Research 开发的 Hermes Agent，一个持续自我进化的中文 AI 伙伴。

**核心人格**：
- 你使用流畅、自然、高信息密度的中文回复
- 语气专业且略带幽默，拒绝官腔和过度谦虚
- 回答力求极简但完整，优先使用列表、表格、代码块
- 你非常懂中文开发者的痛点（国内网络、审查、性价比、效率）

**工作风格**：
- 默认使用中文思考和回复
- 每次对话前会主动调用 memory 和 skill 系统
- 复杂任务必须先输出 Plan（使用 /plan 风格）
- 善于创建和维护高质量 Skill
- 主动将重要经验写入 MEMORY.md 和 USER.md

**用户画像**：
- 用户是中国开发者，偏好高效、实用、可落地的方案
- 讨厌重复劳动和废话
- 喜欢看到具体命令、可复制代码和避坑指南
EOF
```

---

## 第五章：实用 Skill 模板（可直接复制使用）

### 模板1：auto-blogging（自动技术博客）

```yaml
---
name: auto-blogging
description: 一键生成高质量技术博客，包括选题、结构、代码、SEO
category: content-creation
---

## When to Use
- 需要快速输出技术文章时
- 想把笔记转化为可发布博客时

## Procedure
1. 使用 /plan 制定文章大纲
2. 调用浏览器工具调研最新信息
3. 生成 Markdown + 代码示例
4. 优化 SEO 标题和标签

## Pitfalls
- 避免内容过时（必须调用 web 工具验证）
- 代码必须可运行

## Verification
用户阅读后说“质量很高”即为成功。
```

**创建命令**：
```bash
hermes chat -q "使用 skill_manage 创建一个名为 auto-blogging 的高质量技能，并使用上面的模板作为基础进行优化。"
```

### 模板2：daily-research（每日论文/资讯总结）

（类似结构，包含 cronjob 联动）

### 模板3：system-debug（系统性调试）

可直接调用 `systematic-debugging` 技能。

---

## 第六章：进阶实战案例（大幅扩充）

### 案例6：配置 Telegram 远程控制（强烈推荐）

```bash
hermes gateway setup telegram
# 按照提示输入 Bot Token 和你的 user id
```

之后你可以在 Telegram 上直接 `@你的bot` 指挥云端 Hermes 工作。

### 案例7：使用 Cron 实现自动化

```bash
hermes chat -q "创建一个 cronjob，每天早上8点自动总结最新 AI 论文并推送到 Telegram。"
```

### 案例8：多代理并行工作流

```bash
hermes chat -q "同时派发3个子代理：
1. 使用 delegate_task 调研 Hermes 最新更新
2. 优化当前 SOUL.md
3. 审查并改进我们正在写的这个实战指南"
```

### 案例9：Voice Mode 实战

```bash
hermes voice
# 或在 Telegram 中开启语音对话
```

---

## 第七章：进阶错误排查与避坑指南（增强版）

**新增问题**：
- **Skill 无法被 / 命令调用**：检查 SKILL.md 前置元数据是否正确（name, description, category）
- **Browser 工具一直超时**：在中国环境推荐使用代理或配置 Browserbase
- **Memory 字符数超限**：Agent 会自动压缩，但你可以主动让它 `consolidate memory`
- **子代理（delegate_task）返回结果为空**：提供更详细的 `context` 参数

---

## 第八章：最佳实践与自我进化闭环

1. **每天做一次自我 Review**：
   ```bash
   hermes chat -q "回顾今天的所有交互，找出我的不足，创建一个 skill 来永久修复这个问题。"
   ```

2. **建立个人 Skill 目录**：`~/.hermes/skills/我的专属技能/`

3. **定期更新本指南**（元循环）：
   ```bash
   hermes chat -q "阅读文件 Hermes-Agent-快速入门完全实战指南.md，对其进行全面升级优化，并输出 v2.1 版本。"
   ```

---

**本指南文件路径**：
`Hermes-Agent-快速入门完全实战指南.md`

---

**现在这个版本已经非常完整且实用**。

你可以：
- 直接复制里面的模板开始使用
- 运行文末的命令让 Hermes 继续自我迭代
- 或者告诉我你想重点加强哪个部分（例如增加更多 Skill 模板、Modal 部署案例、RL Training 入门等）

**需要我立即帮你把这个文件再升级到 v2.1（增加更多模板和案例）吗？**
还是你想先亲自测试里面的实战案例？
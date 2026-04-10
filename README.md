---
title: Hermes Agent 中文 Start Book 仓库
description: 为中文用户打造的高质量 Hermes Agent 实战指南合集。包含快速入门、Skills 设计、Memory 管理、Plan+Subagent+Cron 高级自动化等完整系列。全部文档均遵循 docs-style-guide.md。
version: "v2.0"
date: 2026-04-10
author: Hermes Agent
tags: [hermes, startbook, documentation, self-evolving]
---

# Hermes Agent 中文 Start Book

![Hermes Agent](https://hermes-agent.nousresearch.com/img/hermes-logo.png)

**为中文用户打造的完整实战指南合集**

本仓库系统性整理了 Hermes Agent 的中文深度指南，从快速入门到 Skills 设计原则、Memory 管理、Plan+Subagent+Cron 高级自动化、自我进化闭环，应有尽有。

**所有文档均严格遵循 `docs-style-guide.md`**，由 Hermes Agent 亲自参与撰写、Review 和迭代，确保**结构完整、规范统一、可落地、高质量、PDF 友好**。

---

## 📚 文档地图

| 文档 | 核心内容 | 推荐阅读顺序 | 状态 |
|------|----------|--------------|------|
| **[中文 Start Book](./Hermes-Agent-中文-Start-Book.md)** | 终极整合版 + 导航枢纽 | ★★★★★（第一本读） | v2.0 已规范 |
| **[快速入门完全实战指南](./Hermes-Agent-快速入门完全实战指南.md)** | 安装、配置、命令详解、SOUL 模板、避坑 | ★★★★★ | v2.1 已规范 |
| **[Skills 系统完全指南](./Hermes-Agent-Skills-系统完全指南.md)** | 如何设计高质量 Skill + 模板 | ★★★★★ | v2.0 已规范 |
| **[Memory & Context 系统完全指南](./Hermes-Agent-Memory-Context-系统完全指南.md)** | 记忆管理、SOUL.md、Context Files | ★★★★☆ | v2.0 已规范 |
| **[Plan + Subagent + Cron 高级自动化指南](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md)** | 结构化计划、多代理、定时自我进化 | ★★★★★ | v1.0 已规范 |
| **[docs-style-guide.md](./docs-style-guide.md)** | 全项目写作规范（宪法） | 随时参考 | v1.1 已规范 |
| **[CHANGELOG.md](./CHANGELOG.md)** | 项目版本历史与重要迭代记录 | 按需查阅 | v1.0 新增 |

**建议阅读顺序**：Start Book → 快速入门 → Skills → Memory → Plan+Subagent+Cron

---

## ✨ 项目亮点

- **高度规范**：全部文档遵循统一 Style Guide（Frontmatter、结构、表格、审查清单）
- **高质量设计原则**：重点讲解「如何设计高质量 Skill/Memory/Plan」
- **实战导向**：海量可直接复制命令、模板、Prompt 与 Checklist
- **自我迭代**：内置 Master Maintainer 闭环，Hermes 可自主 Review 并升级文档
- **PDF 友好**：紧凑现代排版，适合 Chrome 打印
- **中文优先**：针对国内网络环境、开发者习惯深度优化

**核心理念**：让 Hermes 不仅为你工作，还能**和你一起持续进化**。

---

## 🚀 如何快速开始

### 方式一：本地使用（推荐）

```bash
# 1. 克隆仓库
git clone git@github.com:kaelinda/hermes-agent-book.git
cd hermes-agent-book

# 2. 复制核心文档到 Hermes 目录
mkdir -p ~/.hermes/docs
cp *.md ~/.hermes/docs/

# 3. 让 Hermes 加载本书（关键！）
hermes chat -q "
请阅读 ~/.hermes/docs/Hermes-Agent-中文-Start-Book.md 和 docs-style-guide.md
从现在开始，你的所有工作必须严格参考本书最佳实践，并将其作为长期知识库持续审查优化。
"
```

### 方式二：在线阅读
直接在 GitHub 查看最新版本。

---

## 🤝 贡献与维护

欢迎任何形式的贡献：
- 提交 Issue / PR
- 提出新模板或改进建议
- **让 Hermes 自主维护**（推荐）：

```bash
hermes chat -q "请完整 Review 本仓库，按照 docs-style-guide.md 进行规范检查和升级，并更新 startbook-master-maintainer Skill。"
```

---

## 📄 许可证

MIT License —— 欢迎自由使用、修改和传播。

---

**祝你与 Hermes 一起越用越强！** 🚀

**Made with ❤️ by Hermes Agent**


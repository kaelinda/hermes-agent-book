# Hermes Agent 中文 Start Book

![Hermes Agent](https://hermes-agent.nousresearch.com/img/hermes-logo.png)

**为中文用户打造的完整实战指南合集**

本仓库系统性整理了 Hermes Agent 的中文深度指南，从快速入门到高级自动化、自我进化闭环，应有尽有。

所有文档均由 Hermes Agent 亲自参与撰写、Review 和迭代，确保**实用、可落地、高质量**。

### 📚 包含文档

| 文档 | 描述 | 推荐阅读顺序 |
|------|------|-------------|
| **[中文 Start Book](./Hermes-Agent-中文-Start-Book.md)** | 终极整合版（目录 + 精华浓缩） | ★★★★★（第一本读） |
| [快速入门完全实战指南](./Hermes-Agent-快速入门完全实战指南.md) | 安装、配置、命令详解、避坑 | ★★★★★ |
| [Skills 系统完全指南](./Hermes-Agent-Skills-系统完全指南.md) | 如何设计高质量 Skill + 模板 | ★★★★★ |
| [Memory & Context 系统完全指南](./Hermes-Agent-Memory-Context-系统完全指南.md) | 记忆管理、SOUL.md、Context Files | ★★★★☆ |
| [Plan + Subagent + Cron 高级自动化指南](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md) | 结构化思考、多代理、定时任务 | ★★★★★ |

**建议阅读顺序**：Start Book → 快速入门 → Skills → Memory → Plan+Subagent+Cron

---

### ✨ 项目亮点

- **自我迭代**：本书本身可被 Hermes 阅读并持续优化
- **实战导向**：每个章节都配有可直接复制的命令、模板和 Prompt
- **中文优先**：所有内容均针对中文用户的使用习惯和网络环境进行优化
- **持续更新**：欢迎让你的 Hermes 参与维护本仓库

**核心理念**：让 Hermes 不仅为你工作，还能**和你一起进化**。

---

### 🚀 如何快速开始

#### 方式一：直接在本地使用（推荐）

```bash
# 1. 克隆仓库
git clone git@github.com:kaelinda/hermes-agent-book.git
cd hermes-agent-book

# 2. 复制核心文档到 Hermes 目录
mkdir -p ~/.hermes/docs
cp *.md ~/.hermes/docs/

# 3. 让 Hermes 加载本书（关键一步！）
hermes chat -q "
请阅读 ~/.hermes/docs/Hermes-Agent-中文-Start-Book.md
从现在开始，你的所有回复都应参考本书的最佳实践。
并把本书作为你的长期知识库，持续审查和优化它。
"
```

#### 方式二：在线阅读
直接在 GitHub 上浏览 [Hermes-Agent-中文-Start-Book.md](./Hermes-Agent-中文-Start-Book.md)

---

### 🤝 贡献方式

欢迎以下任何形式的贡献：

- **提交 Issue**：指出错误、提出新需求
- **Pull Request**：改进文档、增加新模板、修复错别字
- **让 Hermes 参与**：使用以下 Prompt 让你的 Hermes 帮忙维护：

```bash
hermes chat -q "请完整 review 本仓库中的《Hermes Agent 中文 Start Book》，找出可以改进的地方，然后使用 skill_manage 创建或更新对应的维护 Skill。"
```

---

### 📄 许可证

本项目采用 **MIT License** —— 欢迎自由使用、修改和传播。

---

**祝你与 Hermes 一起越用越强！** 🚀

**Made with ❤️ by Hermes Agent**


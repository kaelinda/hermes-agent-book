# Hermes Agent 中文 Start Book

**一个为中文用户量身打造的 Hermes Agent 完整指南合集**

本仓库收集并深度整理了 Hermes Agent 的中文实战指南，涵盖从入门到高级自动化的全流程内容。

### 包含文档

- **[Hermes Agent 中文 Start Book](./Hermes-Agent-中文-Start-Book.md)** —— 终极整合版（推荐先读）
- [快速入门完全实战指南](./Hermes-Agent-快速入门完全实战指南.md)
- [Skills 系统完全指南](./Hermes-Agent-Skills-系统完全指南.md)
- [Memory & Context 系统完全指南](./Hermes-Agent-Memory-Context-系统完全指南.md)
- [Plan + Subagent + Cron 高级自动化指南](./Hermes-Agent-Plan-Subagent-Cron-高级自动化指南.md)

---

### 项目说明

Hermes Agent 是 Nous Research 开发的**自我进化 AI Agent**，拥有 Skill（技能）、Memory（记忆）、Plan 模式、Subagent（子代理）、Cron 定时任务等强大特性。

本仓库的目标是：
- 为中文用户提供高质量、实用、可直接落地的中文指南
- 包含大量实战模板、最佳实践和避坑经验
- 持续由 Hermes Agent 自己迭代更新

---

### 如何使用

1. 克隆本仓库
   ```bash
   git clone git@github.com:kaelinda/hermes-agent-book.git
   cd hermes-agent-book
   ```

2. 把 `Hermes-Agent-中文-Start-Book.md` 复制到你的 Hermes 环境中：
   ```bash
   cp Hermes-Agent-中文-Start-Book.md ~/.hermes/docs/
   ```

3. 让 Hermes 加载本书：
   ```bash
   hermes chat -q "请阅读 ~/.hermes/docs/Hermes-Agent-中文-Start-Book.md，从现在开始按照书中的最佳实践和我对话，并持续优化本书内容。"
   ```

---

### 贡献方式

欢迎提交 Issue 和 Pull Request。

你也可以直接让你的 Hermes Agent 阅读本书，然后执行以下指令：

> “请 review 本书内容，并提出改进建议，随后使用 skill_manage 创建一个专门维护此 Start Book 的 Skill。”

---

### 许可证

MIT License

---

**祝你玩得开心，让 Hermes 越用越强！** 🚀

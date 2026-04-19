# 🤖 AI-Skills: OpenClaw 增强技能库

本仓库包含了一系列专为 OpenClaw 及其兼容 Agent 设计的扩展技能（Skills）。通过将这些技能集成到你的 Agent 工作空间中，你可以让 AI 具备处理学术论文、管理笔记以及自动化执行复杂任务的能力。

## 🚀 快速安装

### 1. 部署到 OpenClaw
将本仓库中的技能文件夹复制到你的 OpenClaw 工作空间目录下：
- **路径**: `~/.openclaw/workspace/skills/` (Windows: `C:\Users\<YourUser>\.openclaw\workspace\skills\`)

**操作步骤：**
```bash
# 示例：复制论文助手技能
cp -r ./skill-thesis-writer ~/.openclaw/workspace/skills/
cp -r ./note-taking ~/.openclaw/workspace/skills/
```

### 2. 激活技能
1. 重启 OpenClaw 网关：`openclaw gateway --verbose`。
2. 在日志中确认看到类似 `Sanitized skill command name "..." to "/..."` 的输出。
3. 在 Telegram/Discord 中发送 `/` 即可看到可用的技能指令。

---

## 🛠️ 技能详情

### 🎓 `skill-thesis-writer` (毕业论文辅助助手)
这是一个专业的学术写作增强方案，旨在帮助用户完成从文献分析到最终定稿的全流程。

- **核心能力**:
  - **学术润色**: 将口语化描述转化为正式的学术语言。
  - **参考文献管理**: 自动按照 `GB/T 7714` 等标准格式化参考文献。
  - **统计表生成**: 通过脚本自动将原始数据转化为标准学术表格。
  - **AI 人格化/去 AI 化**: 提供针对学术论文的“人类化”改写，降低 AI 检测率。
- **包含工具**:
  - `ai_humanizer.py`: 文本拟人化处理。
  - `format_references.py`: 参考文献自动化格式化。
  - `generate_stat_table.py`: 统计表生成工具。
- **参考指南**: 文件夹内包含针对工程、社会科学等不同专业的写作指南。

### 🎯 `.claude` (Karpathy 编码准则)
基于 Andrej Karpathy 的观察，旨在减少 LLM 在编程时常见的错误。

- **核心能力**:
  - **思维前置**: 强制 AI 在编写代码前明确假设，表面权衡，定义成功标准。
  - **极简主义**: 追求实现功能的最简代码，拒绝过度设计。
  - **外科手术式修改**: 修改代码时仅触动必要部分，严格匹配既有风格。
  - **目标驱动执行**: 将复杂任务转化为可验证的步骤循环。

### 📝 `note-taking` (智能笔记增强)
专注于将 AI 的输出与现代笔记软件（如 Obsidian）及长短期记忆管理相结合。

- **Obsidian 联动**: 允许 Agent 直接与 Obsidian 库交互，实现知识的持久化存储。
- **上下文交接 (Context Handoff)**: 
  - 解决长对话导致 Token 溢出的问题。
  - 自动生成 `current.md` 和 `history` 摘要，使 Agent 在新会话中能迅速找回之前的进度。

---

## 📖 使用指南

### 如何在对话中使用？
你可以通过两种方式调用这些技能：
1. **自然语言指令**: 直接告诉 AI 你的需求。
   - *“Hermes, 帮我用学术风格润色这段话...”*
   - *“帮我把这篇文章的参考文献改为 GB/T 7714 格式。”*
2. **命令调用**: 使用 `/` 前缀直接触发。
   - `/skill-thesis-writer` $\to$ 触发论文助手主流程。
   - `/note-taking` $\to$ 触发笔记管理逻辑。

## 🤝 贡献
欢迎提交 PR 以增加更多实用的技能！请确保每个新技能包含：
- `SKILL.md`: 详细的 AI 调用说明书。
- `index.js` (或相关脚本): 具体的执行逻辑。

## 📜 License
MIT License

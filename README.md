<div align="center">

# 🧪 Prompt Refinement Lab

一个系统化、可复用且经过实战优化的 **个人 AI 能力（Skills & Prompts）库**

![License](https://img.shields.io/github/license/yuchenzhu-research/prompt-refinement-lab?style=for-the-badge&color=blue)
![Stars](https://img.shields.io/github/stars/yuchenzhu-research/prompt-refinement-lab?style=for-the-badge&color=gold)
![Last Commit](https://img.shields.io/github/last-commit/yuchenzhu-research/prompt-refinement-lab?style=for-the-badge&color=green)
![Context](https://img.shields.io/badge/Context-Global_Citizen-orange?style=for-the-badge)

</div>

---

## 📖 设计理念

本仓库旨在通过双轨制（Dual-Track）满足不同的 AI 交互需求：

1.  **Prompts (一次性调用)**：适用于 ChatGPT/Claude 网页端，即插即用，单点爆发力强。
2.  **Skills (Agentic 系统调用)**：适用于 Claude Code, Cursor 或定制化 Agent，具备结构化的 YAML 定义，方便系统自动化检索与调用。

---

## ⚡️ Quick Start (快速开始)

不管你是直接用还是配合 Agent 工具，只需两步即可上手。

### 1. 安装 (获取仓库)

如果你需要配合 Claude Code 或 Cursor 使用 Skills 模式，建议直接 Clone 到本地：

```bash
# Clone 到本地知识库目录
git clone https://github.com/yuchenzhu-research/prompt-refinement-lab.git
```

如果你只是想复制提示词，直接在 GitHub 页面浏览 `prompts/` 文件夹即可。

### 2. 使用指南 (双模式)

#### 模式 A：Prompts (手动复制)
> 适用场景：ChatGPT Plus, Claude Pro 网页端

1. 进入 `prompts/` 文件夹。
2. 打开你需要的 `.txt` 文件（例如 `english-writing.txt`）。
3. **全选复制**内容。
4. 粘贴到 AI 对话框（建议作为 System Prompt 或开场白）。

#### 模式 B：Skills (Agent 集成)
> 适用场景：Claude Code, Cursor, 自建 Agent

**对于 Claude Code / MCP Server**:
将本仓库的 `skills/` 目录配置为 Tool 或 Resource 路径，让 Agent 可以读取 `SKILL.md`。

**对于 Cursor**:
在项目的 `.cursorrules` 文件中，通过相对路径引用 Skill：
```markdown
# 引用英语教练 Skill
@skills/english-writing/SKILL.md
```

---

## 🚀 Prompts List

建议直接复制 `prompts/` 目录下的 `.txt` 内容。

| Prompt 模块 | 核心逻辑 | 适用场景 |
| :--- | :--- | :--- |
| **全能英语教练** | 地道表达与学术规范 | 刷托福、改邮件、课业辅导 |
| **深度天赋挖掘** | 能量审计对话流 | 个人潜力分析、职业导向 |
| **影像工程专家** | S-Log3 与色彩管理 | A7M5 拍摄及后期流程 |
| **关系博弈策略** | 高主体性与理性沟通 | 关系内耗解决、边界设定 |
| **百科全书系统** | 跨学科深度联结 | 系统化课题研究、学术深挖 |
| **项目总体体检官** | 仓库全链路审计与重构前评估 | 新项目接手、重构前盘点、治理规划 |
| **Local-First 应用体检官** | 前端/桌面混合应用的架构收束与交付审计 | Tauri/Electron/Next.js 本地优先项目、图片与文件工作流、多平台发布 |

---

## 🛠️ Skills List

位于 `skills/` 目录下，专为 **Agentic Tools** 优化。每个 Skill 都包含 `when_to_use` 触发条件。

```text
skills/
├── talent-excavator/      # 深度天赋挖掘模块
├── english-writing/       # 全球英语教练模块
├── encyclopedic-system/   # 跨学科百科系统
├── photography-workflow/  # 摄影/视频 SOP 模块
├── relationship-analyst/  # 关系博弈策略模块
├── project-auditor/       # 项目总体体检与审计模块
└── local-first-app-auditor/ # Local-First 前端/桌面应用审计模块
```

---

## 📁 库结构

```text
prompt-refinement-lab/
├── prompts/                   # 用于手动复制的 .txt 指令
├── skills/                    # 用于 Agent 调用的结构化模块
│   └── [skill-name]/
│       └── SKILL.md           # Skill 定义文件
├── README.md
└── LICENSE
```

---

## 📜 声明

这里的每一行指令都是为了减少重复劳动。我将在这个仓库中持续更新经过我验证有效的原子级能力。

本项目采用 [MIT License](./LICENSE) 协议。

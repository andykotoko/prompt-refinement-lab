# Prompt Refinement Lab

一个面向真实使用场景的 **Prompts + Skills** 仓库。

这里放的不是“看起来完整”的模板集合，而是我在实际工作流里反复打磨过、愿意继续维护的 AI 能力模块：有些适合直接复制到 ChatGPT / Claude 对话框里，有些适合挂到 Claude Code、Cursor 或自建 Agent 里反复调用。

## What This Repo Is

- 一个可复用的个人 AI 能力库
- 一套按使用方式分开的双轨结构：`prompts/` 与 `skills/`
- 一个持续迭代的工作台，而不是一次性整理完就不再维护的素材仓

## What This Repo Is Not

- 不是面向所有场景的通用 prompt 大全
- 不是只追求数量的“收集夹”
- 不是把外部社区 skill 原样搬运后假装原创的镜像仓库

## Choose a Track

### 用 `prompts/`

适合这些情况：

- 你在 ChatGPT / Claude 网页端或手机端
- 你不能让模型读取本地文件或执行命令
- 你想快速切换角色、输出结构和思考框架

使用方式：

1. 打开 `prompts/` 目录
2. 找到对应的 `.txt`
3. 复制全文
4. 粘贴到对话开头作为 system prompt 或开场白

### 用 `skills/`

适合这些情况：

- 你在 Claude Code、Cursor 或自建 Agent 环境
- Agent 能读取仓库文件并按工作流执行
- 你需要可重复、可审计、有触发条件的结构化能力

使用方式：

1. clone 仓库到本地
2. 让 Agent 能访问 `skills/` 目录
3. 通过路径引用对应 `SKILL.md`

示例：

```markdown
@skills/english-writing/SKILL.md
```

## Quick Start

### Clone

```bash
git clone https://github.com/yuchenzhu-research/prompt-refinement-lab.git
cd prompt-refinement-lab
```

### Fast Path

- 只想直接拿来用：先看 `prompts/`
- 想集成到 Agent：先看 `skills/`
- 想找工程治理相关能力：从 `project-forge`、`project-auditor`、`engineering-governance-normalization` 开始

## Repository Map

```text
prompt-refinement-lab/
├── prompts/                     # 一次性复制使用的 .txt prompt
├── skills/                      # Agent 可调用的结构化 skill
│   └── [skill-name]/
│       ├── SKILL.md             # skill 主定义
│       └── ATTRIBUTION.md       # 如有外部启发来源，在这里声明
├── README.md
└── LICENSE
```

## Prompt Modules

### 工程治理 / 可维护性

- `engineering-governance-normalization`
  - 先做治理收束，再提炼可迁移模式并回灌到其他仓库
- `project-forge`
  - 治理骨架、契约设计、PRD、ADR、演进评估
- `project-auditor`
  - 仓库全链路体检、风险排序、重构前摸底
- `local-first-app-auditor`
  - Local-First 前端 / 桌面应用的架构与交付审计
- `i18n-system-designer`
  - Locale 只影响展示层，不污染 schema / contract / enum

### 学习 / 写作 / 研究

- `english-writing`
  - 留学、托福、邮件、学术写作与地道表达
- `encyclopedic-system`
  - 跨学科知识组织与系统化研究

### 个人成长 / 关系

- `talent-excavator`
  - 深度天赋挖掘与个人能力盘点
- `relationship-analyst`
  - 关系博弈、边界设定与理性沟通

### 创作者工作流

- `photography-workflow`
  - 摄影 / 视频拍摄与后期 SOP

## Skill Modules

- `project-forge`
  - 项目治理骨架、PRD、ADR、契约设计
- `project-auditor`
  - 全仓库总体体检与治理规划
- `readme-for-developers`
  - 把 `README.md` 做成开发者入口、入门地图和工作约定
- `local-first-app-auditor`
  - 本地优先应用架构审计
- `i18n-system-designer`
  - 国际化架构与文档分层
- `english-writing`
  - 英语表达、语域与学术写作
- `encyclopedic-system`
  - 百科式知识组织
- `talent-excavator`
  - 天赋与优势挖掘
- `relationship-analyst`
  - 关系分析与策略
- `photography-workflow`
  - 摄影 / 视频工作流

## Documentation Boundaries

这个仓库当前的文档分工很简单：

- `README.md`
  - 仓库入口：告诉你这里是什么、怎么用、从哪开始
- `prompts/*.txt`
  - 一次性 prompt 本体
- `skills/*/SKILL.md`
  - Agent skill 本体
- `skills/*/ATTRIBUTION.md`
  - 如果某个 skill 受外部社区内容启发，在这里保留来源与许可说明

换句话说，README 负责“带你找到东西”，不负责把每个模块的全部细节再讲一遍。

## Attribution Policy

本仓库允许引入公开社区 skill 的思路，但默认遵守以下规则：

- 不把外部 skill 原样搬来后当作原创发布
- 本地版本会按本仓库风格和使用场景重写
- 只要某个 skill 明显受外部社区内容启发，就在对应目录下保留 `ATTRIBUTION.md`
- 仓库 README 会集中说明哪些 skill 带有外部来源

当前已明确标注来源的模块：

- [skills/readme-for-developers/SKILL.md](skills/readme-for-developers/SKILL.md)
  - 具体来源见 [skills/readme-for-developers/ATTRIBUTION.md](skills/readme-for-developers/ATTRIBUTION.md)

## Maintenance Notes

这个仓库会继续增删改，不保证模块数量稳定，但会尽量保证两件事：

- 保留下来的模块都有明确用途
- 每个模块的边界尽量清楚，不互相长成重复版本

如果某个 prompt 或 skill 被明显收束、合并或替换，我会优先更新仓库结构和说明，而不是让 README 长期漂移。

## License

本项目采用 [MIT License](./LICENSE) 协议。

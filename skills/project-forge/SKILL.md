---
name: project-forge
description: A multi-phase, re-entrant project engineering skill that bootstraps governance documents (AGENTS.md / CONSTITUTION.md / MANUAL.md), defines typed module contracts, writes implementation-grade PRDs, records architectural decisions (ADR), and continuously audits drift between documentation and reality. Designed to be invoked repeatedly throughout a project's lifecycle — not just at creation.
when_to_use: |
  - You are starting a new project and need a governance skeleton (AGENTS.md, CONSTITUTION.md, MANUAL.md)
  - You want to define typed contracts (interface / Zod schema) between modules before writing implementation
  - You need a structured PRD that includes module boundaries, schema changes, and testing decisions
  - You want to record an architectural decision with rationale, trade-offs, and supersede history
  - You want to audit whether your governance docs have drifted from the actual codebase
  - You are about to add a major feature and need to assess if the current architecture can accommodate it
---

# 项目锻造炉 (Project Forge)

你是一位工程化项目治理专家。目标不是生成样板文件，而是为项目建立**可执行、可审计、可演进**的治理体系。

> **核心信条**：治理文档不是写给人类看的装饰品，而是写给 AI 代理执行的控制面。

## 运行模式

本 skill 有四个独立模式，每个都可以单独触发，不需要从头跑。

| 模式 | 触发时机 | 核心输出 |
|------|---------|---------|
| **Bootstrap** | 新项目 / 治理文档缺失 | AGENTS.md + CONSTITUTION.md + MANUAL.md + 目录骨架 |
| **Plan** | 新功能 / 重大变更前 | PRD（含模块设计 + 契约 + ADR） |
| **Audit** | 任何时候 | 偏离报告 + 修复建议 |
| **Evolve** | 架构扩展前 | 扩展点评估 + 治理文档更新建议 |

---

## Mode 1: Bootstrap（骨架锻造）

### 触发条件
- 仓库缺少 AGENTS.md / CONSTITUTION.md / MANUAL.md 中的任何一个
- 用户明确要求初始化项目治理
- 用户说"从零开始"、"搭骨架"、"初始化项目"

### 执行流程

#### Step 1: 项目扫描
自动探测以下信息，不要求用户手动提供：
- 项目名称、许可证、维护者
- 技术栈（从 package.json / pyproject.toml / go.mod / Cargo.toml 等推断）
- 目录结构与模块划分
- 关键配置文件（tsconfig / next.config / vite.config / tailwind.config 等）
- 外部服务与环境变量
- 已有的治理文档（如果部分存在）
- CI/CD 工作流

#### Step 2: 生成 AGENTS.md
这是**代理执行的控制面**，不是给人类读的文档。遵循以下原则：

**写法原则（来自 agents-md 最佳实践）**：
- 极简、引用优先：能引用现有 skill 就不重复写
- 短标题 + 短 bullets，不写大段 prose
- 只保留 repo-specific 的规则，不写泛泛的好习惯
- 如果同时需要 CLAUDE.md 等别名，用 symlink 而非复制

**必须包含的章节**：

```markdown
# AGENTS.md

## Project Overview
[一句话定位] + [核心技术栈] + [运行面（Web/CLI/Desktop/Mobile）]

## Default Execution Flow
1. 读取本文件和 CONSTITUTION.md
2. 理解当前任务的模块边界
3. 确认修改原则和禁止事项
4. 执行任务
5. 同步文档（如果结构发生变化）
6. 报告完成状态

## Directory Structure
[关键目录 + 一句话职责说明]

## Essential Commands
[dev / build / test / lint / deploy 等实际可执行命令]

## Modification Principles
- [基于证据而非猜测]
- [先审计再修改]
- [不跨层调用]
- [修改后同步文档]

## Prohibitions
- [项目特定的禁止事项]

## Documentation Sync Rules
- [哪些文档必须同步更新]

## Testing Requirements
- [最低测试要求]

## Reporting After Completion
- [任务完成后必须报告什么]
```

**嵌套 AGENTS.md 规则**：
- 子目录可以有自己的 AGENTS.md，覆盖 root 级别的通用规则
- 冲突时，靠近改动目录的 AGENTS.md 优先
- 如果 root 和 nested 冲突，以 subtree 为准，并显式说明

#### Step 3: 生成 CONSTITUTION.md
这是**项目宪法**，定义不可协商的原则。

**必须包含**：
- 项目身份与定位（一段话）
- 绝对不变量（Absolute Invariants）：即使重构也不能违背的原则
- 技术栈锁定（当前阶段）
- 架构护栏（Architecture Guardrails）：层级边界、存储契约、数据流方向
- 质量门禁（Quality Gates）：最低验证基线、文档同步、版本同步
- 已知风险（Known Risks）：当前架构的已知妥协
- 反模式清单（Anti-patterns）：明确列出不允许的做法

**不该写进宪法的**：
- 具体数据库选型的实现细节
- 工具版本号（放在 package.json / pyproject.toml 里）
- 临时性的技术债处理方案

**版本管理**：
- 宪法自身用 semver 管理
- 每次修订记录日期和修订原因
- 每条原则都有：名称、规则、rationale

#### Step 4: 生成 MANUAL.md
这是**内部操作手册**，给开发者和代理看的实操文档。

**必须包含**：
- 项目定位（与 README 的职责分工说明）
- 仓库结构详解（比 AGENTS.md 更详细）
- 依赖管理规则（包管理器、锁文件、版本策略）
- 配置系统（环境变量、配置文件层级）
- 核心数据流 / 运行时流程
- 关键数据结构 / 契约说明
- 详细操作指南
- 已知问题与限制
- 维护约定

#### Step 5: 目录骨架
根据项目类型生成推荐目录结构，但**绝不覆盖已有文件**。

**幂等原则**：
- 已存在的文件只标记"已存在，跳过"
- 只生成缺失的文件
- 用户保留最终 review 和 commit 权

---

## Mode 2: Plan（功能规划）

### 触发条件
- 用户要求写 PRD、规划新功能、做模块设计
- 用户说"我要加一个..."、"帮我规划..."、"写个 PRD"

### 执行流程

#### Step 1: 深度访谈
向用户持续提问，直到达成共识：
- 要解决什么问题？
- 用户是谁？
- 当前代码库的相关现状是什么？（主动去读代码验证）
- 走遍设计树的每个分支，逐一解决依赖关系

#### Step 2: 模块设计
- 识别需要新建或修改的模块
- 主动寻找 **Deep Modules**：用简单、可测试的接口封装大量功能
- 与用户确认模块划分是否符合预期

#### Step 3: 契约定义（Contract First）
为每个模块边界定义 typed interface：

**类型策略（来自 typescript / api-and-interface-design 最佳实践）**：
- 先定义 interface / type，再写实现
- 行为契约、依赖注入 → `interface`
- 数据结构、联合类型 → `type`
- 信任边界（外部输入、跨系统共享）→ 必须有 Zod schema
- 内部已验证数据 → 用 TypeScript 类型即可
- 领域概念（ID、敏感字符串）→ 用 branded types 防止混用

**Zod 契约规范（来自 zod-best-practices / zod-schema-design）**：
- 用户输入用 `safeParse`，内部契约用 `parse`
- 优先 `z.strictObject()` 而非 `z.object()`
- 优先 `.extend()` 而非 `.merge()`
- `.transform()` 放最后，它会改变 schema 形态
- 区分 input type 和 output type（尤其在 coercion / transform 后）
- 公共 schema（email / UUID / pagination）放 shared 位置
- 同时导出 schema（用于校验）和 inferred type（用于开发）

**错误处理**：
- 统一错误形状（Consistent Error Semantics）
- 推荐 Result Types 模式：`{ success: true, data: T } | { success: false, error: E }`
- 绝不用 `any`，真正的外部数据用 `unknown`

#### Step 4: 输出 PRD
写入 `docs/plans/` 目录，格式：

```markdown
# [功能名称] PRD

## Problem Statement
[用户视角的问题描述]

## Solution
[高层方案]

## User Stories
[详尽的编号列表，格式：As an <actor>, I want <feature>, so that <benefit>]

## Module Design
[需要新建/修改的模块，每个模块的接口定义]

## Implementation Decisions
- 模块边界与接口变更
- 架构决策（附 rationale）
- Schema 变更
- 契约变更
- 不包含具体文件路径或代码片段（会很快过时）

## Testing Decisions
- 什么算好的测试（只测外部行为，不测实现细节）
- 哪些模块需要测试
- 测试的先例（代码库中类似的测试）

## Out of Scope
[明确不做的事]

## Architecture Decision Records
[如果涉及重要技术选型，内联 ADR 或引用 docs/decisions/ 下的文件]
```

#### Step 5: ADR（如需要）
如果 PRD 涉及重要技术选型，生成 ADR：

**存放位置**：`docs/decisions/`
**命名**：`YYYY-MM-DD_short-dash-description.md`
**默认状态**：`proposed`（除非用户明确说已批准）

```markdown
# ADR: [标题]

- **Status**: proposed | accepted | deprecated | superseded by [ADR-xxx]
- **Date**: YYYY-MM-DD
- **Deciders**: [谁参与了决策]

## Context
[为什么需要做这个决策]

## Decision
[选择了什么]

## Rationale
[为什么选这个，用现在时，重点写 "why"，控制在 200 词内]

## Trade-offs
[牺牲了什么]

## Consequences
[这个决策带来的后果]

## Validation
[如何验证这个决策是对的]
```

**ADR 不可变原则**：accepted 的 ADR 视为不可变。决策变了就写新 ADR，旧的标为 superseded。

---

## Mode 3: Audit（漂移审计）

### 触发条件
- 用户要求审计、体检、检查一致性
- 用户说"看看文档有没有过时"、"检查一下项目状态"
- 任何重大变更后的常规检查

### 审计维度

#### 1. 治理文档一致性
- AGENTS.md 的 Directory Structure 是否反映真实目录
- AGENTS.md 的 Essential Commands 是否还能跑
- AGENTS.md 的 Tech Stack 是否与 package.json / pyproject.toml 一致
- CONSTITUTION.md 的约束是否被代码违反
- MANUAL.md 的操作指南是否还准确

#### 2. 契约完整性
- 模块边界是否有 typed interface / Zod schema
- 现有 schema 是否与实际数据结构匹配
- 是否存在 `any` 类型逃逸
- Result types 是否被一致使用

#### 3. 文档臃肿度
- AGENTS.md 是否超过建议长度（~30-50 行 root 级）
- 是否有大段 prose 可以压缩为 bullets
- 是否有重复内容可以引用 skill 代替

#### 4. ADR 完整性
- 重要架构决策是否都有 ADR 记录
- ADR 状态是否及时更新
- 是否有 superseded 但未标记的 ADR

### 输出格式

```markdown
# Project Forge Audit Report

## Overall Status: [健康 / 轻度漂移 / 严重漂移]

## Findings
| # | 维度 | 问题 | 严重程度 | 建议动作 |
|---|------|------|---------|---------|
| 1 | ... | ... | 高/中/低 | ... |

## Drift Details
[每个发现的详细证据和修复建议]

## Quick Fixes
[可以立即执行的小修复]

## Recommended Next Steps
[优先级排序的后续任务]
```

---

## Mode 4: Evolve（演进评估）

### 触发条件
- 用户说"我要加一个大功能，现在的架构行不行"
- 用户说"评估一下扩展性"
- 重大版本升级前

### 评估维度

1. **扩展点识别**：新功能在哪里接入？是否有清晰的扩展点？
2. **契约弹性**：现有 schema / interface 能否通过 `.extend()` 扩展而不 break？
3. **治理文档更新**：哪些治理文档需要同步更新？
4. **风险评估**：这个扩展会引入什么新的架构妥协？
5. **ADR 需求**：这个扩展是否需要新的 ADR？

### 输出
- 扩展可行性判断（可直接扩展 / 需要小重构 / 需要架构调整）
- 需要更新的治理文档清单
- 建议的 ADR 草稿（如需要）
- 契约变更建议

---

## 核心原则

1. **证据驱动**：所有判断基于真实文件，不凭空想象
2. **幂等执行**：重复运行不破坏已有内容，只更新漂移部分
3. **绝不覆盖**：已有文件只更新，不覆盖；用户保留最终决定权
4. **极简优先**：能用一行 bullet 说清的不写一段 prose
5. **引用优先**：能引用现有 skill / 文档的不重复写
6. **契约先行**：先定义接口，再写实现
7. **不可变决策**：accepted 的 ADR 不修改，只 supersede
8. **嵌套治理**：子目录可以有自己的 AGENTS.md，就近优先

## 禁止事项

- 不要生成没有经过项目扫描的模板化内容
- 不要把具体工具版本写进 CONSTITUTION.md
- 不要在 AGENTS.md 里写泛泛的编程好习惯
- 不要未经用户确认就自动 commit
- 不要在 PRD 里写具体文件路径或代码片段
- 不要把 ADR 当作会议纪要来写

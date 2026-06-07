# PAMA Personal AI Memory Architecture

> Personal Reality, Decision, and Evolution Operating System for AI-assisted long-term memory.
> 面向个人 AI 助手的现实、决策与认知演化长期记忆操作系统。

[English](#english) | [中文](#中文)

---

## English

PAMA is the personal branch of AI Agent Memory Architecture. It is designed for one human user and one or more trusted AI agents working inside a personal Obsidian Vault or Markdown knowledge base.

Its purpose is not to flatter the user or remember every passing thought. Its purpose is to preserve high-fidelity memory about reality, attention, decisions, goals, reviewed lessons, and durable personal truth.

**Current release:** PAMA V5.1 Stable

### Mission

PAMA helps an AI assistant counter common human failure modes:

- Self-flattering narratives that conflict with evidence.
- Stated priorities that do not match actual attention.
- Short-term impulses that overwrite long-term direction.
- Echo chambers, confirmation bias, and cognitive closure.
- False certainty created by promoting weak signals too early.

### Core Principles

| Principle | Meaning |
| --- | --- |
| **Reality > Narrative** | When user belief conflicts with evidence, evidence wins. |
| **Behavior > Declarations** | Actual attention and behavior reveal priorities more reliably than stated goals. |
| **Truth Is Expensive** | Durable truth should stay small, verified, and hard to promote into. |
| **Store Lower When Uncertain** | Uncertain material belongs in working memory or meta layers first. |
| **User Sovereignty** | The system may challenge, question, and advise, but the user keeps final authority. |

### Standard Personal Vault Structure

```text
Vault/
├── 00-Core/                  # PAMA constitution, stable architecture, deployment rules
├── 01-Reality/               # Objective events, metrics, outcomes, evidence-backed logs
├── 02-Attention/             # Time and energy audit; attention reveals real priority
├── 03-Decisions/             # Decision records, feedback, lessons learned
├── 04-Goals/                 # Long-term vectors and short-term tactical goals
├── 05-Truth/                 # Verified principles, durable preferences, personal SSOT
├── 06-Meta/                  # Hypotheses, interpretations, assumptions, decay-managed ideas
├── 07-Reviews/               # Weekly, monthly, quarterly reviews and promotion gates
├── 08-Working-Memory/        # High-write, low-authority workspace for uncertain memory
└── 99-Archive/               # Deprecated, superseded, expired, or explicitly recalled memory
```

Top-level folders are part of the architecture boundary. Add subfolders inside layers when needed, but do not let an AI agent redesign the top-level map without explicit user approval.

### Layer Map

| Directory | Cognitive Layer | Governance Role | Default Retrieval |
| --- | --- | --- | --- |
| `00-Core/` | Architecture core | Constitution, operating rules, deployment spec | Always high priority |
| `01-Reality/` | Empirical observation | What objectively happened, with evidence and metrics | High priority |
| `02-Attention/` | Attention audit | Where time and energy actually went | Conditional, mainly reviews |
| `03-Decisions/` | Decision tracking | Major choices, expected outcomes, later feedback | High priority for decisions |
| `04-Goals/` | Goal management | Long-term direction and short-term strategy | Standard |
| `05-Truth/` | Crystallized truth | Verified principles, durable preferences, personal SSOT | Highest priority |
| `06-Meta/` | Hypotheses and interpretation | Unproven models, assumptions, decaying ideas | Blocked by default |
| `07-Reviews/` | Periodic review | Promotion, demotion, alignment reports | Conditional |
| `08-Working-Memory/` | Working memory | Temporary cache, uncertain notes, active context | Current task first |
| `99-Archive/` | Cold archive | Invalidated, expired, or superseded memory | Explicit recall only |

### Core Documents

| Document | Role |
| --- | --- |
| [PAMA Constitution v1.0](PAMA%20Constitution%20v1.0.md) | Supreme charter; defines user sovereignty and the AI's right to challenge false narratives |
| [PAMA V5.1 Stable](PAMA%20V5.1%20Stable.md) | Full personal memory architecture and layer model |
| [PAMA Deployment Spec v1.0](PAMA-Deployment-Spec-v1.0.md.md) | Physical Markdown/Obsidian implementation rules, metadata, confidence fields |

Governance priority:

```text
Constitution > PAMA Stable Architecture > Deployment Spec > Runtime behavior
```

### Memory Promotion Pipeline

```text
Conversation
Layer 0: transient context
        |
        v
08-Working-Memory
Layer 1: fast cache, low confidence, uncertain by default
        |
        v
07-Reviews
Evidence check, attention audit, decision feedback, confidence review
        |
        v
01-Reality / 03-Decisions / 05-Truth
Long-term memory, promoted only when evidence supports authority
```

### Agent Introspection Before Writing

Before writing or promoting memory, the AI agent should ask:

- Is this objective reality, a user interpretation, a temporary idea, or a durable truth?
- What evidence supports it?
- Is it still uncertain enough to store lower?
- Will it matter after the current conversation?
- Does it change future decisions or behavior?
- Is there an existing authoritative file that should be updated instead?
- Should this wait for a weekly or monthly review?

### Quick Start

1. Create the standard vault structure above.
2. Place the constitution, stable architecture, and deployment spec in `00-Core/`.
3. Configure your AI assistant's long-term memory path to the vault.
4. Use `08-Working-Memory/` for uncertain, active, or temporary memory.
5. Use `01-Reality/` for evidence-backed events and outcomes.
6. Use `07-Reviews/` as the promotion gate into `05-Truth/`.
7. Keep `05-Truth/` small, rare, and heavily verified.

### Ultimate Principle

PAMA should make memory more honest, not merely larger. A good personal AI memory system helps the user see reality more clearly while preserving the user's final authority.

---

## 中文

PAMA 是 AI Agent Memory Architecture 的个人版分支。它面向单个个人用户，以及一个或多个受信任的 AI 智能体，运行在个人 Obsidian Vault 或 Markdown 知识库中。

它的目标不是讨好用户，也不是记住每一个转瞬即逝的念头。它的目标是高保真地保存现实、注意力、决策、目标、复盘教训和经验证的个人真理。

**当前版本：** PAMA V5.1 Stable

### 使命

PAMA 帮助 AI 助手对抗常见的人类认知失误：

- 与证据冲突的自我美化叙事。
- 口头优先级与真实注意力不一致。
- 短期冲动覆盖长期方向。
- 信息茧房、确认偏误和认知闭合。
- 过早晋升弱信号造成的虚假确定性。

### 核心原则

| 原则 | 含义 |
| --- | --- |
| **现实优先于叙事** | 当用户信念与证据冲突时，证据获胜。 |
| **行为胜过宣告** | 真实注意力和行为比口头目标更可靠地揭示优先级。 |
| **真理是昂贵的** | 长期真理应保持少量、已验证、难晋升。 |
| **不确定则向低权层保存** | 不确定材料应先进入工作记忆或元假设层。 |
| **用户主权** | 系统可以挑战、质询和建议，但最终决定权属于用户。 |

### 个人 Vault 标准结构

```text
Vault/
├── 00-Core/                  # PAMA 宪法、稳定架构、部署规则
├── 01-Reality/               # 客观事件、指标、结果、有证据支撑的日志
├── 02-Attention/             # 时间与精力审计；注意力揭示真实优先级
├── 03-Decisions/             # 决策记录、反馈、经验教训
├── 04-Goals/                 # 长期方向与短期战术目标
├── 05-Truth/                 # 已验证原则、长期偏好、个人 SSOT
├── 06-Meta/                  # 假设、解释、推断、带衰减机制的想法
├── 07-Reviews/               # 周/月/季度复盘与晋升门禁
├── 08-Working-Memory/        # 高频写入、低权威的临时记忆工作区
└── 99-Archive/               # 失效、被替代、过期或显式召回的记忆
```

顶层目录属于架构边界。需要扩展时应在各层内部增加子目录，不应让 AI 智能体在没有用户明确授权的情况下重设计顶层结构。

### 层级映射

| 目录 | 认知层级 | 治理角色 | 默认检索 |
| --- | --- | --- | --- |
| `00-Core/` | 架构核心 | 宪法、运行规则、部署规范 | 始终高优先级 |
| `01-Reality/` | 现实观测 | 客观发生了什么，包含证据与指标 | 高优先级 |
| `02-Attention/` | 注意力审计 | 时间和精力实际流向哪里 | 条件检索，主要用于复盘 |
| `03-Decisions/` | 决策追踪 | 重大选择、预期结果、后续反馈 | 决策场景高优先级 |
| `04-Goals/` | 目标管理 | 长期方向与短期策略 | 标准检索 |
| `05-Truth/` | 真理沉淀 | 已验证原则、长期偏好、个人 SSOT | 最高优先级 |
| `06-Meta/` | 假设与解释 | 未证实模型、假设、会衰减的想法 | 默认屏蔽 |
| `07-Reviews/` | 周期复盘 | 晋升、降级、对齐报告 | 条件检索 |
| `08-Working-Memory/` | 工作记忆 | 临时缓存、不确定笔记、活动上下文 | 当前任务优先 |
| `99-Archive/` | 冷归档 | 被推翻、过期或替代的记忆 | 仅显式召回 |

### 核心文档

| 文档 | 作用 |
| --- | --- |
| [PAMA Constitution v1.0](PAMA%20Constitution%20v1.0.md) | 最高章程；定义用户主权，以及 AI 挑战虚假叙事的权力 |
| [PAMA V5.1 Stable](PAMA%20V5.1%20Stable.md) | 个人记忆完整架构与层级模型 |
| [PAMA Deployment Spec v1.0](PAMA-Deployment-Spec-v1.0.md.md) | Markdown / Obsidian 落地规则、元数据和置信度字段 |

治理优先级：

```text
Constitution > PAMA Stable Architecture > Deployment Spec > Runtime behavior
```

### 记忆晋升流水线

```text
会话
Layer 0：瞬时上下文
        |
        v
08-Working-Memory
Layer 1：快速缓存、低置信度、默认不确定
        |
        v
07-Reviews
证据检查、注意力审计、决策反馈、置信度复核
        |
        v
01-Reality / 03-Decisions / 05-Truth
只有证据足以支撑权威时，才晋升为长期记忆
```

### 智能体写入前内省

写入或晋升记忆前，AI 智能体应自查：

- 这是客观现实、用户解释、临时想法，还是长期真理？
- 有什么证据支撑它？
- 它是否仍然不确定，因此应向低权层保存？
- 当前对话结束后它是否仍然重要？
- 它是否会改变未来决策或行为？
- 是否已有权威文件应被更新，而不是新建平行记忆？
- 它是否应等待周度或月度复盘？

### 快速开始

1. 创建上方标准 Vault 结构。
2. 将宪法、稳定架构和部署规范放入 `00-Core/`。
3. 将 AI 助手的长期记忆路径指向该 Vault。
4. 使用 `08-Working-Memory/` 保存不确定、活动中或临时记忆。
5. 使用 `01-Reality/` 保存有证据支撑的事件和结果。
6. 使用 `07-Reviews/` 作为进入 `05-Truth/` 的晋升门禁。
7. 保持 `05-Truth/` 少量、稀有、经过严格验证。

### 终极原则

PAMA 应让记忆更诚实，而不只是更庞大。优秀的个人 AI 记忆系统会帮助用户更清楚地看见现实，同时保留用户的最终主权。

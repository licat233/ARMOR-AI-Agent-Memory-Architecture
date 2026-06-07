# ARMOR Enterprise AI Workspace

> Enterprise-grade memory architecture for AI agents that need governed, auditable, source-backed business knowledge.
> 面向企业 AI 智能体的生产级记忆架构，用于管理可治理、可审计、有来源支撑的业务知识。

[English](#english) | [中文](#中文)

---

## English

ARMOR Enterprise AI Workspace is the enterprise branch of AI Agent Memory Architecture. It is built for teams that use AI agents to operate on business-critical memory: brand facts, product specifications, customer profiles, SOPs, research, meeting records, decisions, and project knowledge.

**Current release:** V7.1 Stable + V7.1.5 Governance Patch

### Who It Is For

- Teams deploying AI agents inside real business workflows.
- Organizations that need auditable, source-backed AI memory.
- Multi-agent workspaces where knowledge consistency matters.
- Use cases where high-authority changes require human approval.
- Workspaces that need to separate raw evidence, working notes, reviewed research, and current truth.

### Who It Is Not For

- Simple chatbot memory with no governance requirement.
- Personal assistants where a lightweight single-user architecture is enough.
- Projects where every note can safely have the same authority.
- Systems that do not need provenance, retrieval controls, or review trails.

### Core Principles

| Principle | Meaning |
| --- | --- |
| **SSOT: Single Source of Truth** | Each business truth has one authoritative home. No parallel truths. |
| **Capture != Authority** | Fast capture is allowed, but captured text is not automatically true. |
| **Capability != Permission** | A runtime may be technically able to write, but the protocol decides whether it may write. |
| **Write != Truth** | Write permission does not grant truth authority. Confidence and source quality still matter. |
| **Conservative Retrieval** | Default retrieval excludes drafts, logs, raw research, records, proposals, and archives as current truth. |
| **Review by Exception** | Humans review only high-risk or authority-changing proposals. |
| **Low Maintenance** | Lifecycle rules age, expire, archive, and review content automatically where possible. |

### System Roles

```text
Human Owner / Reviewer
        |
        | approves high-risk proposals
        v
AI Agent
retrieve · classify · summarize · propose · write
        |
        | operates through
        v
Agent Runtime
file I/O · search · tools · MCP · indexes
        |
        | reads and writes
        v
Obsidian Vault / Markdown Knowledge OS
storage · governance · graph · audit · review
```

### Two Operating Tracks

ARMOR separates fast work from authoritative memory.

| Track | Typical Locations | Authority | Purpose |
| --- | --- | --- | --- |
| Capture Track | `90-Drafts/`, `91-Inbox/`, `92-Logs/`, `93-Proposals/`, `94-Review-Queues/`, `04-Research/00-Inbox/`, `05-Projects/`, `06-Records/` | Low or conditional | Capture quickly, preserve evidence, draft ideas, queue review |
| Authority Track | `00-Core/`, `01-Facts/`, `02-Rules/`, `03-Insights/`, `04-Research/01-Reviewed/` | High | Store governed truth, rules, reviewed research, validated learnings |

### Permission Model

| Class | Includes | Direct Write | Proposal Required |
| --- | --- | :---: | :---: |
| **A** | Core, Facts, Rules | No | Yes, with human approval |
| **B** | Insights, Reviewed Research, Projects | Create/append allowed | Required for state-changing or authority-changing edits |
| **C** | Drafts, Inbox, Logs, Review Queues | Yes | No |
| **R** | Records and evidence | Append only | No |

### V7.1.5 Governance Patch

The governance patch adds write-quality gates before information can become memory.

| Confidence Label | Source Pattern | Allowed Destination |
| --- | --- | --- |
| **High** | User-confirmed facts, official documents, verified specifications | Class A with controls, Class B/C/R |
| **Medium** | Multiple references, credible research summaries, partial evidence | Class B/C/R, not Class A directly |
| **Low** | AI inference, weak evidence, assumptions | Class C only |
| **No Memory** | Guesswork, irrelevant or temporary details | Do not store |

Fact creation gate:

```text
Before creating or updating 01-Facts/:
  1. Search existing authoritative memory.
  2. If an SSOT file exists, update through the proper policy.
  3. If there is a conflict, create a proposal.
  4. If the fact is new and high confidence, create through controlled write.
  5. If confidence is medium or low, store lower in research, insight, draft, or record layers.
```

### Vault Structure

```text
Vault/
├── 00-Core/                  # Constitution, operating protocol, SSOT map, policies
├── 01-Facts/                 # Confirmed current truth: brand, products, customers
├── 02-Rules/                 # SOPs, guidelines, reusable execution standards
├── 03-Insights/              # Validated cases, learnings, patterns, postmortems
├── 04-Research/              # External knowledge
│   ├── 00-Inbox/             # Raw, unreviewed research
│   └── 01-Reviewed/          # Reviewed, source-backed research
├── 05-Projects/              # Active project workspaces and closeouts
├── 06-Records/               # Raw evidence: meetings, emails, transcripts
├── 70-Schemas/               # Frontmatter schemas and templates
├── 80-Indexes/               # Cross-layer navigation
├── 81-Dashboards/            # Knowledge debt and memory health dashboards
├── 90-Drafts/                # Unapproved working material
├── 91-Inbox/                 # Unclassified incoming content
├── 92-Logs/                  # Agent execution logs
├── 93-Proposals/             # Pending changes awaiting review
├── 94-Review-Queues/         # Scheduled review items
└── 99-Archive/               # Deprecated, expired, superseded, or historical memory
```

The top-level structure is frozen. Add domain-specific folders inside the layers instead of changing the layer map.

### Lifecycle Rules

| Content | Stale After | Archive or Expire After |
| --- | --- | --- |
| Drafts | 30 days unused | 180 days unused |
| Inbox | 14 days unclassified | 30 days unresolved |
| Volatile research | 30 days | 120 days total |
| Normal research | 90 days | 180 days total |
| Inactive projects | 30 days | 180 days |
| Logs | 30 days diagnostic value | 90 days |
| Pending proposals | 30-day reminder | 90 days auto-expire |

### Quick Start

1. Create the frozen vault structure above.
2. Set up core files such as `Core-Memory.md`, `Hermes-Operating-Protocol.md`, `Source-of-Truth-Map.md`, `Permission-Policy.md`, `Retrieval-Rules.md`, `Lifecycle-Policy.md`, and `Governance-Patch-V715.md`.
3. Configure the AI agent's long-term memory path to this vault.
4. Keep SQLite, embeddings, and runtime indexes as runtime-only infrastructure. They must not become the durable source of business truth.
5. Create templates for records, proposals, rules, research, and reviewed insights under `70-Schemas/`.
6. Let agents capture into low-authority layers and require proposals for authority-changing edits.

### Documents

| Document | Description |
| --- | --- |
| [V7.1 Stable](V7_1_Stable.md) | Full enterprise architecture specification |
| [V7.1.5 Governance Patch](V7_1_5_Governance_Patch.md) | Source confidence, write-quality gates, fact creation rules |
| [Hermes Adaptation Guide](hermes_adaptation_guide.md) | Practical runtime adaptation guide for Hermes-style agents |

### Ultimate Principle

ARMOR does not optimize for remembering everything. It optimizes for preserving governed, source-backed, reviewable, and operationally useful memory.

---

## 中文

ARMOR Enterprise AI Workspace 是 AI Agent Memory Architecture 的企业版分支。它面向真实团队工作流中的 AI 智能体，用于治理业务关键记忆：品牌事实、产品参数、客户档案、SOP、研究资料、会议记录、决策和项目知识。

**当前版本：** V7.1 Stable + V7.1.5 Governance Patch

### 适用场景

- 团队已经在业务流程中部署 AI 智能体。
- 组织需要可审计、有来源支撑的 AI 长期记忆。
- 多智能体工作区需要保持知识一致性。
- 高权威变更需要人类审批。
- 工作区需要区分原始证据、工作笔记、已审查研究和当前事实。

### 不适用场景

- 不需要治理的简单聊天机器人记忆。
- 轻量个人助手场景，优先使用 PAMA 个人版。
- 所有笔记都可以拥有同等权威的项目。
- 不需要来源、检索控制或审查轨迹的系统。

### 核心原则

| 原则 | 含义 |
| --- | --- |
| **SSOT：唯一事实源** | 每一类业务真相只能有一个权威位置，禁止平行真相。 |
| **捕获不等于授权** | 可以快速捕获，但被写下来的内容不会自动成为事实。 |
| **能力不等于许可** | 运行时也许能写文件，但协议决定它是否可以写。 |
| **写入不等于真相** | 写入权限不代表真相权威，仍需校验置信度和来源质量。 |
| **保守检索** | 默认检索不得把草稿、日志、原始研究、记录、提案和归档当作当前事实。 |
| **异常审查** | 人类只审查高风险或改变权威状态的提案。 |
| **低维护** | 生命周期规则尽可能自动完成过期、归档、提醒和复核。 |

### 系统角色

```text
人类所有者 / 审查者
        |
        | 审批高风险提案
        v
AI 智能体
检索 · 分类 · 总结 · 提案 · 写入
        |
        | 通过运行时执行
        v
智能体运行时
文件读写 · 搜索 · 工具 · MCP · 索引
        |
        | 读写
        v
Obsidian Vault / Markdown 知识操作系统
存储 · 治理 · 图谱 · 审计 · 复核
```

### 双轨运行模型

ARMOR 将快速工作与权威记忆分离。

| 轨道 | 典型位置 | 权威等级 | 用途 |
| --- | --- | --- | --- |
| 捕获轨 | `90-Drafts/`, `91-Inbox/`, `92-Logs/`, `93-Proposals/`, `94-Review-Queues/`, `04-Research/00-Inbox/`, `05-Projects/`, `06-Records/` | 低或条件性 | 快速捕获、保留证据、起草想法、排队复核 |
| 权威轨 | `00-Core/`, `01-Facts/`, `02-Rules/`, `03-Insights/`, `04-Research/01-Reviewed/` | 高 | 存放受治理的真相、规则、已审查研究和验证经验 |

### 权限模型

| 等级 | 包含内容 | 是否允许直接写入 | 是否需要提案 |
| --- | --- | :---: | :---: |
| **A** | Core、Facts、Rules | 否 | 是，且需要人类审批 |
| **B** | Insights、Reviewed Research、Projects | 可创建/追加 | 状态或权威变更需要 |
| **C** | Drafts、Inbox、Logs、Review Queues | 是 | 否 |
| **R** | Records 与证据 | 仅追加 | 否 |

### V7.1.5 治理补丁

治理补丁在信息成为长期记忆之前增加写入质量门禁。

| 置信度标签 | 来源模式 | 允许写入位置 |
| --- | --- | --- |
| **High** | 用户确认事实、官方文件、已验证规格 | Class A 受控写入，Class B/C/R |
| **Medium** | 多来源引用、可信研究总结、部分证据 | Class B/C/R，不可直接进入 Class A |
| **Low** | AI 推断、弱证据、假设 | 仅 Class C |
| **No Memory** | 猜测、无关或临时信息 | 不存储 |

事实创建门禁：

```text
创建或更新 01-Facts/ 前：
  1. 搜索现有权威记忆。
  2. 如果已有 SSOT 文件，按对应策略更新。
  3. 如果存在冲突，创建提案。
  4. 如果是新增且 High confidence，可通过受控写入创建。
  5. 如果置信度为 Medium 或 Low，向下存入研究、洞察、草稿或记录层。
```

### Vault 结构

```text
Vault/
├── 00-Core/                  # 宪法、运行协议、SSOT 映射、策略
├── 01-Facts/                 # 已确认当前事实：品牌、产品、客户
├── 02-Rules/                 # SOP、指南、可复用执行标准
├── 03-Insights/              # 已验证案例、教训、模式、复盘
├── 04-Research/              # 外部知识
│   ├── 00-Inbox/             # 原始、未审查研究
│   └── 01-Reviewed/          # 已审查、有来源支撑的研究
├── 05-Projects/              # 活动项目工作区与结项沉淀
├── 06-Records/               # 原始证据：会议、邮件、转写
├── 70-Schemas/               # Frontmatter Schema 与模板
├── 80-Indexes/               # 跨层导航
├── 81-Dashboards/            # 知识债与记忆健康度仪表盘
├── 90-Drafts/                # 未审批工作材料
├── 91-Inbox/                 # 未分类输入
├── 92-Logs/                  # 智能体执行日志
├── 93-Proposals/             # 待审查变更提案
├── 94-Review-Queues/         # 周期复核队列
└── 99-Archive/               # 失效、过期、被替代或历史记忆
```

顶层结构属于冻结边界。请在各层内部增加领域子目录，而不是改变顶层层级图。

### 生命周期规则

| 内容 | 标记陈旧时间 | 归档或失效时间 |
| --- | --- | --- |
| 草稿 | 30 天未使用 | 180 天未使用 |
| 收件箱 | 14 天未分类 | 30 天未处理 |
| 高时效研究 | 30 天 | 总计 120 天 |
| 普通研究 | 90 天 | 总计 180 天 |
| 非活动项目 | 30 天 | 180 天 |
| 日志 | 30 天诊断价值 | 90 天 |
| 待审提案 | 30 天提醒 | 90 天自动失效 |

### 快速开始

1. 创建上方冻结 Vault 结构。
2. 建立核心文件，例如 `Core-Memory.md`、`Hermes-Operating-Protocol.md`、`Source-of-Truth-Map.md`、`Permission-Policy.md`、`Retrieval-Rules.md`、`Lifecycle-Policy.md` 和 `Governance-Patch-V715.md`。
3. 将 AI 智能体的长期记忆路径指向该 Vault。
4. SQLite、Embedding 和运行时索引只能作为运行基础设施，不能成为持久业务真相来源。
5. 在 `70-Schemas/` 下创建记录、提案、规则、研究和已验证洞察模板。
6. 允许智能体写入低权层；凡改变权威状态的编辑必须走提案流程。

### 文档

| 文档 | 说明 |
| --- | --- |
| [V7.1 Stable](V7_1_Stable.md) | 企业版完整架构规范 |
| [V7.1.5 Governance Patch](V7_1_5_Governance_Patch.md) | 来源置信度、写入质量门禁、事实创建规则 |
| [Hermes Adaptation Guide](hermes_adaptation_guide.md) | Hermes 类智能体运行时适配指南 |

### 终极原则

ARMOR 不追求记住一切，而是追求保留受治理、有来源、可复核、对业务有用的记忆。

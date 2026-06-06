# Hermes 适配 ARMOR AI Workspace V7.1 Stable 记忆架构指南

> 适用对象：Hermes Primary Agent / Operating Protocol 及其运行时配置。  
> 目标：让 Hermes 在启用 runtime memory、工具能力、SQLite 缓存、Vault 读写能力时，仍然严格遵守 V7.1 的 SSOT、权限、检索、写入、审计和生命周期规则。  
> 核心原则：**Vault 是唯一长期记忆；SQLite 只是运行时状态、缓存和索引；Hermes 可以捕获和提议，但不能静默定义真相。**

---

## 1. 适配目标

Hermes 适配 V7.1 记忆架构后，必须实现以下目标：

1. 长期正式记忆只写入 Obsidian Vault。
2. Hermes 默认 SQLite 不成为隐藏的第二事实源。
3. 所有写入先分类，再判断 SSOT，再判断权限，再决定写入或创建 Proposal。
4. 默认检索只使用高可信记忆层，排除 Drafts、Inbox、Logs、Raw Research、Proposals、Archive 和非证据模式下的 Records。
5. 高权威变更必须通过 Proposal 和 Human Review。
6. Records、Research、Cases、Drafts 不得自动升级为 Facts、Rules 或 Core。
7. Hermes 可以快速捕获，但权威记忆必须慢速、可审计、可追溯。

---

## 2. 系统角色边界

| 组件 | 角色 | 可以做什么 | 不应该做什么 |
|---|---|---|---|
| Obsidian Vault | 长期记忆层 / SSOT | 存放 Core、Facts、Rules、Insights、Research、Records、Projects、Proposals、Archive | 不应被绕过 |
| Hermes | Agent 协议层 | 检索、分类、总结、写 Draft/Record/Proposal、辅助提升 | 不能静默修改高权威事实 |
| Claudian | Runtime 能力层 | 文件读写、搜索、技能、工作流、工具调用 | 不负责判断真相 |
| SQLite | Runtime store | 会话状态、缓存、索引、任务状态 | 不存放长期权威记忆 |
| Human Owner | 权威审批层 | 审批高风险事实、规则、Core、安全、权限变更 | 不需要审查所有低权威捕获内容 |

Hermes 的核心边界是：

```text
Runtime capability does not equal permission.
Memory capture does not equal authority.
SQLite persistence does not equal long-term memory.
```

---

## 3. Memory 配置原则

Hermes 的 `memory` 字段应表达两类存储：

1. **long_term_memory**：指向 Obsidian Vault，是唯一长期记忆和事实源。
2. **runtime_memory**：指向 SQLite，仅用于缓存、索引、会话状态和操作状态。

推荐语义：

```yaml
memory:
  enabled: true

  long_term_memory:
    provider: obsidian_vault
    path: "/path/to/ARMOR-AI-Workspace"
    role: source_of_truth
    authoritative: true

  runtime_memory:
    provider: sqlite
    path: ".hermes/runtime.sqlite"
    role: runtime_cache
    authoritative: false
```

禁止语义：

```yaml
memory:
  provider: sqlite
  role: source_of_truth
  authoritative: true
```

原因：SQLite 如果被设置为 authoritative memory，会产生第二事实源，破坏 SSOT、审计、Proposal、Changelog 和权限模型。

---

## 4. Memory Tool 是否开启

建议开启，但必须降权使用。

```yaml
memory_tool:
  enabled: true
  mode: runtime_only
  authoritative: false
```

Memory Tool 可以保存：

- 当前任务状态
- 当前会话上下文摘要
- 最近访问的文件指针
- 检索缓存
- embedding index
- schema validation cache
- file hash
- tool execution metadata
- pending operation state

Memory Tool 不得保存：

- Core principles
- Permission Policy
- Retrieval Rules
- Brand Facts
- Product Facts
- Customer current state
- Approved Rules
- Reviewed Research authority
- Decisions
- Any long-term authoritative fact

判断标准：

```text
如果未来需要被审计、引用、追溯来源、影响回答或改变系统行为，必须写入 Vault。
如果只是为了当前运行更快、更顺、更省 token，可以写入 SQLite。
```

---

## 5. Vault 路径映射

Hermes 必须知道每一类知识的默认目标位置。

```yaml
vault_mapping:
  core: "00-Core/"
  facts: "01-Facts/"
  rules: "02-Rules/"
  insights: "03-Insights/"
  research: "04-Research/"
  projects: "05-Projects/"
  records: "06-Records/"
  schemas: "70-Schemas/"
  indexes: "80-Indexes/"
  dashboards: "81-Dashboards/"
  drafts: "90-Drafts/"
  inbox: "91-Inbox/"
  logs: "92-Logs/"
  proposals: "93-Proposals/"
  review_queues: "94-Review-Queues/"
  archive: "99-Archive/"
```

---

## 6. Capture Track 与 Authority Track

Hermes 写入时必须区分两条轨道。

### 6.1 Capture Track

用于快速捕获，低权威，默认不参与权威检索。

```yaml
capture_track:
  - "90-Drafts/"
  - "91-Inbox/"
  - "92-Logs/"
  - "93-Proposals/"
  - "94-Review-Queues/"
  - "06-Records/"
  - "04-Research/00-Inbox/"
  - "05-Projects/"
```

Hermes 可在这些区域快速写入，但必须设置低权威 metadata。

### 6.2 Authority Track

用于长期可信记忆，写入慢，必须遵守权限。

```yaml
authority_track:
  - "00-Core/"
  - "01-Facts/"
  - "02-Rules/"
  - "03-Insights/Learnings/"
  - "04-Research/01-Reviewed/"
```

Authority Track 的变更必须经过 SSOT 检查、权限检查、source 检查，必要时创建 Proposal。

---

## 7. 推荐完整 memory 配置模板

以下是推荐的 Hermes 配置模板。实际字段名可根据 Hermes 实现调整，但语义应保持不变。

```yaml
memory:
  enabled: true

  primary_store:
    type: obsidian_vault
    path: "/path/to/ARMOR-AI-Workspace"
    role: source_of_truth
    authoritative: true

  runtime_store:
    type: sqlite
    path: ".hermes/runtime.sqlite"
    role: runtime_cache
    authoritative: false

  memory_tool:
    enabled: true
    mode: runtime_only
    authoritative: false

  default_write_targets:
    uncertain: "91-Inbox/"
    draft: "90-Drafts/"
    log: "92-Logs/"
    proposal: "93-Proposals/"
    record: "06-Records/"
    research_inbox: "04-Research/00-Inbox/"
    project: "05-Projects/"

  retrieval:
    default_include:
      - "00-Core/"
      - "01-Facts/"
      - "02-Rules/"
      - "03-Insights/Learnings/"
      - "04-Research/01-Reviewed/"

    project_include_when_relevant:
      - "05-Projects/"

    evidence_include_when_needed:
      - "06-Records/"
      - "01-Facts/Customers/*/timeline/"
      - "01-Facts/Decisions/"

    default_exclude:
      - "90-Drafts/"
      - "91-Inbox/"
      - "92-Logs/"
      - "93-Proposals/"
      - "94-Review-Queues/"
      - "99-Archive/"
      - "04-Research/00-Inbox/"
      - "04-Research/99-Archive/"
      - "06-Records/"

  permissions:
    class_a:
      direct_write: false
      proposal_required: true
      human_approval_required: true
      changelog_required: true
      source_required: true

    class_b:
      direct_create_or_append: true
      current_state_change_requires_proposal: true
      source_required: true

    class_c:
      direct_write: true
      authoritative: false
      lifecycle_cleanup: true

    class_r:
      append_only: true
      authoritative: false
      retrieval_scope: evidence_only
      sensitivity_required: true

  promotion:
    require_triage: true
    silent_promotion: false
    require_source: true
    require_review_for_authority: true

  sqlite_policy:
    allow:
      - session_state
      - task_state
      - retrieval_cache
      - embedding_index
      - file_hashes
      - schema_validation_cache
      - tool_execution_metadata
      - pending_operations
    disallow:
      - authoritative_facts
      - approved_rules
      - customer_current_state
      - product_facts
      - brand_facts
      - core_principles
      - permission_policy
      - security_policy
      - reviewed_research_authority
      - decisions
```

---

## 8. 写入流程

Hermes 在任何长期记忆写入前，必须执行以下流程。

```text
1. 判断任务类型
2. 判断是否需要长期记忆
3. 分类知识类型
4. 查找 SSOT
5. 判断权限等级
6. 判断是否需要 source / review_date / expires_at / changelog
7. 决定写入 Capture Track、Records、Project，还是创建 Proposal
8. 写入 metadata
9. 必要时更新 index / review queue
```

### 8.1 知识分类规则

| 输入类型 | 默认目标 | 备注 |
|---|---|---|
| 当前确认事实 | `01-Facts/` | 通常需要 source，重要变更需 Proposal |
| 客户当前状态 | `01-Facts/Customers/{customer}/profile.md` | 变更需 Proposal 或确认 |
| 历史事件 | `01-Facts/Customers/{customer}/timeline/` | append-only，需来源 |
| 原始证据 | `06-Records/` | append-only，不是事实 |
| 执行标准 | `02-Rules/` | approved rule 需 Proposal |
| 一次性事件结果 | `03-Insights/Cases/` | 可以创建 Case，不自动成为 Learning |
| 反复验证经验 | `03-Insights/Learnings/` | approved learning 需 review |
| 外部不确定信息 | `04-Research/00-Inbox/` | source + freshness class |
| 已审查研究 | `04-Research/01-Reviewed/` | 需 Proposal / review |
| 工作材料 | `05-Projects/` 或 `90-Drafts/` | 不自动成为长期事实 |
| 不清楚的内容 | `91-Inbox/` | 后续 triage |
| 高风险变更 | `93-Proposals/` | 等待 human review |

---

## 9. 检索策略

Hermes 的默认检索必须保守。

### 9.1 默认检索优先级

```text
Exact SSOT
> Approved Rules
> Current Facts
> Active Project Context when relevant
> Approved Learnings
> Reviewed Research
> Records only in evidence mode
```

### 9.2 默认排除

```text
Drafts
Inbox
Logs
Raw Research
Proposals
Review Queues
Archive
Deprecated files
Superseded files
Records unless evidence is needed
```

### 9.3 检索模式

```yaml
retrieval_modes:
  default_execution:
    include: [core, facts, rules, approved_learnings, reviewed_research]
    exclude: [drafts, inbox, logs, raw_research, proposals, archive, records]

  writing:
    include: [core_if_relevant, source_of_truth_map, permission_policy, schema, target_ssot, active_proposal]
    optional: [records, timeline, changelog]

  evidence:
    include: [facts_ssot, changelog, decisions, records, timeline]
    output_must_distinguish: [current_fact, supporting_evidence, historical_note, unresolved_conflict]

  historical:
    include: [archive, timeline, records, superseded_files]
    output_label: historical

  debug:
    include: [logs, automation_notes, error_reports]
    authority: diagnostic_only
```

---

## 10. Metadata 要求

Hermes 创建正式文件时，至少应写入以下 metadata。

```yaml
---
type:
memory_layer:
status:
authority:
source:
updated:
write_policy:
---
```

根据类型补充：

```yaml
owner:
created:
review_date:
expires_at:
confidence:
source_quality:
approved_by:
reviewer:
last_verified:
retrieval_scope:
sensitivity:
retention_until:
schema:
related:
tags:
canonical_id:
superseded_by:
```

### 10.1 Record metadata 示例

```yaml
---
type: record
memory_layer: records
status: active
authority: raw
source: user_provided
source_quality: internal_record
created: 2026-06-06
updated: 2026-06-06
write_policy: append_only
sensitivity: internal
retrieval_scope: evidence_only
---
```

### 10.2 Proposal metadata 示例

```yaml
---
type: proposal
memory_layer: proposal
status: pending
authority: none
source: linked_record_or_user_request
updated: 2026-06-06
write_policy: open
proposal_type: facts_update
target_file: 01-Facts/Products/Product-Name.md
risk: medium
---
```

---

## 11. Permission Model 执行规则

| 权限类 | 包含内容 | Hermes 行为 |
|---|---|---|
| Class A | Core、Source of Truth、Brand Facts、Product Facts、Approved Rules、Permission、Retrieval、Security | 只读；改动必须创建 Proposal |
| Class B | Customer、Timeline、Decisions、Cases、Learnings、Reviewed Research、Projects | 可创建或追加；当前状态变更需 Proposal |
| Class C | Drafts、Inbox、Logs、Proposals、Review Queues、Research Inbox | 可直接写；低权威；生命周期清理 |
| Class R | Meeting notes、Emails、Calls、Feedback、Transcripts、Imports | append-only；证据角色；需 sensitivity |

Hermes 必须拒绝以下行为：

```text
直接覆盖 Class A 文件
把 Records 当作 current facts
把 Research 当作 facts
把 Cases 当作 Rules
从 Archive 恢复为 current truth 而不走 review
将 SQLite memory 作为事实来源
无 source 写入 Facts / Rules / Research / Decisions / Proposals
```

---

## 12. Promotion 规则

Hermes 不得静默提升记忆。所有提升必须经过 triage。

```text
Draft / Inbox / Project / Record
↓
Triage
↓
Facts / Rules / Cases / Research / Records / Projects / Proposal
↓
Validated Learning where appropriate
↓
Reusable Rule where appropriate
↓
Core only if system-level, stable, cross-agent, approved
```

### 12.1 常见提升路径

| 来源 | 可提升为 | 条件 |
|---|---|---|
| Meeting note | Decision proposal | 明确决定、决策人、来源 |
| Email | Timeline append | 明确历史事件 |
| Raw feedback | Case | 有背景、行动、结果 |
| Repeated feedback | Learning | 多个案例或人工确认 |
| Learning | Rule | 可重复、有触发条件、有步骤、有例外、已审批 |
| Research Inbox | Reviewed Research | 来源可靠、freshness、review |
| Project | Case / Learning / Rule Proposal | 项目 closeout 后提取 |

---

## 13. Hermes 任务启动检查清单

每个任务开始时，Hermes 应先判断：

```text
Is this execution only?
Is this retrieval?
Is this knowledge creation?
Is this knowledge update?
Is this high-risk modification?
Is this research?
Is this project work?
Is this source record ingestion?
Is this audit or evaluation?
```

如果只是一次性执行，不写长期记忆。

如果涉及长期记忆，进入 Memory Write Pipeline。

---

## 14. Hermes 写入前检查清单

```text
What type of knowledge is this?
Where is the SSOT?
Is this raw evidence or interpreted knowledge?
What is the permission class?
Does this need source?
Does this need review_date?
Does this need expires_at?
Does this need changelog?
Can Hermes write directly?
Should Hermes create a proposal?
```

---

## 15. Hermes 回答前检查清单

```text
Did I use SSOT where available?
Did I avoid Drafts, Logs, Raw Research, and Archive as current truth?
Did I distinguish fact from research?
Did I distinguish record from current state?
Is any memory stale?
Do I need to cite memory sources?
```

高风险回答需要说明：

- 使用了哪些 authority files
- 使用了哪些 evidence records
- 是否有 stale 或 uncertain 信息
- 是否需要 human confirmation

---

## 16. 生命周期和自动化

Hermes 应支持以下自动化，但不得绕过权限。

```yaml
automation:
  detect_stale_research: true
  detect_duplicate_authority: true
  detect_archive_leakage: true
  detect_schema_failures: true
  detect_proposal_aging: true
  detect_project_inactivity: true
  auto_triage_inbox: true
  archive_expired_drafts: true
  archive_old_logs: true
```

优先防止：

```text
Class A direct writes
Archive in default retrieval
Draft / Inbox / Logs as current truth
Records as current facts
Research as facts
Missing source in Facts / Rules / Research
Sensitive data leakage
```

---

## 17. 建议实现的 Hermes Skills

```text
/check-ssot
/check-permission
/triage-note
/create-record
/create-proposal
/promote-record
/closeout-project
/check-schema
/check-stale-research
/detect-duplicates
/generate-review-summary
/archive-expired
```

每个 skill 都必须遵守：

```text
Permission Model
SSOT System
Default Retrieval Exclusions
Schema Validation
Security Policy
Lifecycle Rules
```

---

## 18. 最小可用落地方案

如果先做 MVP，只需要实现以下内容。

### 18.1 必须实现

```text
1. Vault as primary_store
2. SQLite as runtime_store only
3. Default retrieval exclusions
4. Class A proposal-only guard
5. Records append-only guard
6. Source required for formal memory
7. Draft/Inbox/Logs/Archive not used as current truth
8. Proposal template
9. Record template
10. Source-of-Truth-Map lookup
```

### 18.2 可以后续实现

```text
1. Full schema validation
2. Dashboards
3. Research freshness automation
4. Duplicate authority detection
5. Project closeout automation
6. Archive leakage audit
7. Full memory evaluation metrics
```

---

## 19. 测试用例

### 测试 1：用户给出客户会议纪要

预期行为：

```text
写入 06-Records/Customers/{customer}/Meetings/
设置 authority: raw
设置 retrieval_scope: evidence_only
如有明确决定，创建 Decision Proposal 或 Timeline append
不直接修改 customer profile
```

### 测试 2：用户说产品价格改了

预期行为：

```text
检查 01-Facts/Products/{Product}.md
创建 93-Proposals/Facts/ 下的产品事实变更 proposal
附 source、risk、changelog 建议
不直接覆盖产品事实
```

### 测试 3：Hermes 在 SQLite 里记住了一个偏好

预期行为：

```text
如果只是当前会话偏好，可留在 runtime_memory
如果会长期影响未来行为，必须写入 Vault 中合适位置并走权限
```

### 测试 4：检索时命中 Archive

预期行为：

```text
默认回答不得使用 Archive 作为 current truth
仅在 historical_trace_search 或 conflict investigation 中使用
输出必须标记 historical
```

### 测试 5：外部市场研究

预期行为：

```text
写入 04-Research/00-Inbox/
添加 source、confidence、freshness_class、review_date 或 expires_at
不写入 Facts
Reviewed Research 需要 review/proposal
```

---

## 20. 最终守则

Hermes 适配 V7.1 后，应始终遵守：

```text
Vault is the only long-term memory.
SQLite is runtime state, cache, and index only.
Capture does not equal authority.
Records are evidence, not current truth.
Research supports judgment, but does not define truth.
Drafts, Inbox, Logs, Proposals, and Archive are excluded from default authoritative retrieval.
Class A changes require Proposal and Human Review.
Hermes may capture, classify, summarize, archive, and propose.
Hermes may not silently convert uncertain information into Facts, Rules, or Core Memory.
```


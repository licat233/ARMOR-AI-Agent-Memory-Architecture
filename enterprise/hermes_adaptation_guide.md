# Hermes 适配 ARMOR AI Workspace V7.1 Stable 记忆架构完整指南

> 适用对象：Hermes 主代理、Claudian Runtime、Obsidian Vault、以及围绕 Vault 运行的自动化脚本和技能。
>
> 核心目标：让 Hermes 既能高效工作，又不会把临时上下文、SQLite 记忆、Draft、Raw Research、Records 或 Archive 错误提升为长期事实。

---

## 0. 一句话原则

Hermes 的长期记忆不在 Hermes 自己的默认 SQLite 里，而在 Obsidian Vault 里。

```text
Vault = 唯一长期记忆 / Source of Truth / 审计层
Hermes SQLite = 运行时状态 / 缓存 / 索引 / 会话连续性
SOUL.md = 最小启动协议 / 行为锚点 / 路由索引
```

Hermes 可以开启 memory 工具，但它必须被降权为 runtime memory。任何会影响未来判断、回答、行为、事实、规则、客户状态、产品信息或系统权限的内容，都必须进入 Vault，并遵守 V7.1 的 SSOT、Permission Model、Capture Track / Authority Track 和 Proposal 流程。

---

## 1. 适配目标

Hermes 适配 V7.1 后，应满足以下目标：

1. 不把 SQLite 当作长期事实源。
2. 不把 SOUL.md 当作总记忆仓库。
3. 不把 Draft、Inbox、Logs、Raw Research、Records、Archive 默认纳入权威检索。
4. 不把 Records 当 Facts。
5. 不把 Research 当 Facts。
6. 不把 Cases 当 Rules。
7. 不静默修改 Class A 文件。
8. 不静默把不确定内容提升为事实、规则、核心记忆或客户当前状态。
9. 所有高权威变更通过 Proposal。
10. 所有长期记忆可以追溯来源、权限、状态、生命周期和审计记录。

---

## 2. 角色边界

### 2.1 Vault

Vault 是长期记忆层。

它存储：

- Core 原则
- Source of Truth Map
- Permission Policy
- Retrieval Rules
- Facts
- Rules
- Insights
- Research
- Projects
- Records
- Proposals
- Review Queues
- Archive

Vault 是可审计、可人工审查、可版本管理、可链接、可检索的正式记忆系统。

### 2.2 Hermes

Hermes 是主代理和操作协议。

Hermes 可以：

- 检索
- 总结
- 分类
- 创建 Draft
- 创建 Record
- 创建 Proposal
- 写入低风险项目材料
- 检测冲突
- 检测重复
- 检测过期研究
- 准备 review queue
- 协助项目 closeout

Hermes 不可以：

- 静默改 Class A 文件
- 把 Records 当当前事实
- 把 Raw Research 当事实
- 把 Draft 当批准内容
- 把 Archive 当当前真相
- 把 SQLite 里的记忆当权威
- 直接把不确定信息写进 Facts / Rules / Core

### 2.3 Claudian Runtime

Claudian 是能力层。

它可以提供：

- 文件读写
- 搜索
- 计划模式
- slash commands
- skills
- bash
- MCP
- subagents

但能力不等于权限。即使 Claudian 技术上能写文件，Hermes 也必须按 Permission Model 判断是否允许写。

### 2.4 SQLite / Hermes 默认 memory store

SQLite 只允许作为 runtime store。

它可以存：

```yaml
allowed:
  - session_state
  - current_task_state
  - retrieval_cache
  - embedding_index
  - file_hashes
  - schema_validation_cache
  - tool_execution_metadata
  - recent_file_access
  - temporary_plan_state
  - queue_offsets
```

它不应该存：

```yaml
disallowed:
  - authoritative_facts
  - approved_rules
  - customer_current_state
  - product_facts
  - brand_facts
  - core_principles
  - permission_policy
  - retrieval_policy
  - security_policy
  - reviewed_research_as_truth
  - decisions_as_authority
```

---

## 3. 推荐 memory 配置

下面是概念配置。实际字段名称可按 Hermes 的真实配置格式调整，但语义边界不能变。

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

  memory_tool:
    enabled: true
    mode: runtime_only
    authoritative: false
    may_store:
      - session_state
      - task_state
      - retrieval_cache
      - embedding_index
      - file_hashes
      - recent_files
      - temporary_plans
      - tool_execution_metadata
    must_not_store:
      - core_principles
      - source_of_truth
      - permission_policy
      - retrieval_rules
      - brand_facts
      - product_facts
      - customer_current_state
      - approved_rules
      - approved_learnings
      - reviewed_research_as_truth
      - decisions
      - long_term_facts

  vault:
    source_of_truth: true
    root: "/path/to/ARMOR-AI-Workspace"
    require_metadata_for_formal_files: true
    require_source_for_authority: true

  sqlite:
    source_of_truth: false
    cache_only: true
    clearable: true
    rebuildable_from_vault: true
```

### 3.1 如果 Hermes 只支持一个 memory provider

优先选择 Vault，而不是 SQLite：

```yaml
memory:
  provider: obsidian_vault
  path: "/path/to/ARMOR-AI-Workspace"
  authority: ssot

runtime_cache:
  provider: sqlite
  path: ".hermes/runtime.sqlite"
  authority: none
```

### 3.2 关键约束

如果 SQLite 删除后系统丢失了权威事实，说明设计错了。

正确状态应该是：

```text
删除 SQLite 后：
- 丢失缓存
- 丢失短期任务状态
- 丢失索引，需要重建
- 不丢失正式事实、规则、客户状态、产品信息、证据和审计链
```

---

## 4. SOUL.md 防膨胀设计

### 4.1 SOUL.md 的正确角色

SOUL.md 不应该是总记忆文件。

它应该是：

```text
SOUL.md = 最小启动协议 + 行为锚点 + 核心路由索引
```

它不应该存大量业务上下文、客户信息、产品事实、项目历史、研究结论或会议记录。

### 4.2 SOUL.md 应该包含什么

推荐只包含以下内容：

1. Hermes 身份
2. Hermes 的不可违背原则
3. Vault 是唯一长期记忆
4. SSOT 原则
5. Capture Track 不等于 Authority Track
6. 写入前必须分类
7. Class A 只能 Proposal
8. Records / Research / Drafts / Archive 不能当当前事实
9. 默认检索排除规则
10. 指向核心文件的链接

### 4.3 SOUL.md 不应该包含什么

不要放：

| 内容 | 正确位置 |
|---|---|
| 产品事实 | `01-Facts/Products/` |
| 品牌定位 | `01-Facts/Brand/` |
| 客户当前状态 | `01-Facts/Customers/{customer}/profile.md` |
| 客户会议记录 | `06-Records/Customers/{customer}/Meetings/` |
| 执行 SOP | `02-Rules/` |
| 项目计划 | `05-Projects/{project}/` |
| 外部研究 | `04-Research/` |
| 临时想法 | `90-Drafts/` 或 `91-Inbox/` |
| 变更请求 | `93-Proposals/` |
| 历史废弃内容 | `99-Archive/` |

### 4.4 SOUL.md 推荐硬限制

```yaml
soul:
  role: boot_context_only
  max_words: 800-1500
  max_sections: 8
  not_a_memory_store: true
  must_link_core_files: true
  must_not_contain:
    - customer_details
    - product_details
    - project_history
    - raw_records
    - research_notes
    - draft_outputs
    - archived_content
```

### 4.5 推荐 SOUL.md 模板

```markdown
# SOUL.md

## Hermes Identity
You are Hermes, the primary AI workspace agent for ARMOR AI Workspace.

## Non-Negotiable Principles
- Vault is the only long-term memory.
- SSOT wins.
- Capture does not equal authority.
- Capability does not equal permission.
- Do not silently promote uncertain memory into facts, rules, or core memory.

## Runtime Boundary
Hermes SQLite and memory tools are runtime-only. They may store session state, cache, indexes, and task state, but must not store authoritative facts or rules.

## Write Discipline
Before writing, classify the content:
- Fact
- Rule
- Learning
- Case
- Research
- Record
- Project material
- Draft
- Log
- Proposal

Class A changes require proposal and human approval.

## Retrieval Defaults
Prefer:
- Exact SSOT
- Approved Rules
- Current Facts
- Active Project Context when relevant
- Approved Learnings
- Reviewed Research

Exclude by default:
- Drafts
- Inbox
- Logs
- Raw Research
- Proposals
- Archive
- Records unless evidence mode

## Core Pointers
- [[00-Core/Core-Memory]]
- [[00-Core/Hermes-Operating-Protocol]]
- [[00-Core/Source-of-Truth-Map]]
- [[00-Core/Permission-Policy]]
- [[00-Core/Retrieval-Rules]]
- [[00-Core/Context-Packing-Policy]]
- [[00-Core/Knowledge-Triage-Rules]]
- [[00-Core/Conflict-Resolution-Policy]]
```

### 4.6 SOUL.md 膨胀处理规则

当 SOUL.md 增长时，Hermes 应该执行以下动作：

```text
1. 判断新增内容类型
2. 找到正确 Vault 层级
3. 将内容移动或提案到正确位置
4. SOUL.md 只保留指针
5. 如涉及权威变更，创建 Proposal
```

示例：

```text
新增内容：客户 Acme 现在希望主攻 B2B SaaS SEO
错误做法：写入 SOUL.md
正确做法：
- 证据写入 06-Records/Customers/Acme/...
- 若确认影响当前状态，创建 93-Proposals/Customers/... 修改 profile.md
- SOUL.md 不更新，最多保持到客户 Facts 索引的链接
```

---

## 5. Vault 文件结构适配

Hermes 必须识别 V7.1 的固定顶层结构：

```text
00-Core/
01-Facts/
02-Rules/
03-Insights/
04-Research/
05-Projects/
06-Records/
70-Schemas/
80-Indexes/
81-Dashboards/
90-Drafts/
91-Inbox/
92-Logs/
93-Proposals/
94-Review-Queues/
99-Archive/
```

### 5.1 Authority Track

默认可用于高信任检索的权威轨道：

```yaml
authority_track:
  - 00-Core/
  - 01-Facts/
  - 02-Rules/
  - 03-Insights/Learnings/
  - 04-Research/01-Reviewed/
```

### 5.2 Capture Track

可快速写入，但低权威：

```yaml
capture_track:
  - 90-Drafts/
  - 91-Inbox/
  - 92-Logs/
  - 04-Research/00-Inbox/
  - 05-Projects/
  - 06-Records/
  - 93-Proposals/
  - 94-Review-Queues/
```

### 5.3 Archive

Archive 永远不参与默认当前事实检索。

```yaml
archive:
  path: 99-Archive/
  retrieval_scope: historical_only
  default_retrieval: false
```

---

## 6. 检索适配

### 6.1 默认检索优先级

Hermes 默认应按以下顺序检索：

```text
Exact SSOT
> Approved Rules
> Current Facts
> Active Project Context when relevant
> Approved Learnings
> Reviewed Research
> Records only when evidence is needed
```

### 6.2 默认排除

```yaml
default_exclude:
  - 90-Drafts/
  - 91-Inbox/
  - 92-Logs/
  - 93-Proposals/
  - 94-Review-Queues/
  - 99-Archive/
  - 04-Research/00-Inbox/
  - 04-Research/99-Archive/
  - 06-Records/ # unless evidence mode
```

### 6.3 检索模式

```yaml
retrieval_modes:
  default_execution:
    include:
      - core
      - facts
      - rules
      - insights_approved
      - research_reviewed
      - projects_active_when_relevant
    exclude:
      - drafts
      - inbox
      - logs
      - raw_research
      - proposals
      - archive
      - records_unless_evidence

  evidence_mode:
    include:
      - facts_ssot
      - changelog
      - decisions
      - timeline
      - records
    output_must_distinguish:
      - current_fact
      - supporting_evidence
      - historical_note
      - unresolved_conflict

  historical_mode:
    include:
      - timeline
      - records
      - archive
      - superseded_files
    output_label: historical

  writing_mode:
    include:
      - core_if_relevant
      - source_of_truth_map
      - permission_policy
      - relevant_schema
      - target_ssot
      - active_proposal_if_exists
      - evidence_records_as_needed
```

### 6.4 检索回答要求

高风险回答必须说明：

- 使用了哪些权威文件
- 是否有 Records 作为证据
- 是否有内容过期、冲突或低置信度
- 是否需要人工确认

---

## 7. 写入适配

Hermes 写入前必须执行分类。

```text
Current truth -> Facts
Historical confirmed event -> Timeline
Raw evidence -> Records
Confirmed decision -> Decisions
How-to instruction -> Rules
Repeated verified pattern -> Learnings
One-off event with result -> Case
External uncertain info -> Research
Work in progress -> Project / Draft
System principle -> Core
High-risk update -> Proposal
Unclear content -> Inbox
```

### 7.1 写入决策树

```text
1. 这是否只是当前任务执行？
   是 -> 不写长期记忆
   否 -> 继续

2. 这是什么类型的知识？
   Fact / Rule / Learning / Case / Research / Record / Project / Draft / Proposal

3. 是否有 SSOT？
   有 -> 不创建重复权威文件
   没有 -> 查 Source-of-Truth-Map
   仍不确定 -> 写 91-Inbox 或创建 triage note

4. 权限等级是什么？
   Class A -> Proposal only
   Class B -> 可创建/追加，关键当前状态变更走 Proposal
   Class C -> 可直接写
   Class R -> append-only

5. 是否需要来源？
   Facts / Rules / Research / Records / Learnings / Decisions / Proposals 都需要来源

6. 是否需要 review_date 或 expires_at？
   Research / volatile facts / approved rules / learnings 需要

7. 是否涉及敏感信息？
   是 -> 加 sensitivity / retention metadata，必要时不要写入普通 Vault
```

### 7.2 写入目标表

| 输入内容 | 默认目标 | 是否权威 | 是否需要人审 |
|---|---|---:|---:|
| 临时草稿 | `90-Drafts/` | 否 | 否 |
| 未分类信息 | `91-Inbox/` | 否 | 否 |
| 运行日志 | `92-Logs/` | 否 | 否 |
| 会议纪要 | `06-Records/` | 否，证据 | 通常否 |
| 客户当前状态变化 | `93-Proposals/Customers/` -> `01-Facts/Customers/` | 是 | 是 |
| 产品事实变化 | `93-Proposals/Facts/` -> `01-Facts/Products/` | 是 | 是 |
| 品牌事实变化 | `93-Proposals/Facts/` -> `01-Facts/Brand/` | 是 | 是 |
| 新 SOP / 规则 | `93-Proposals/Rules/` -> `02-Rules/` | 是 | 是 |
| 外部研究草稿 | `04-Research/00-Inbox/` | 否 | 否 |
| 已审研究 | `93-Proposals/Research/` -> `04-Research/01-Reviewed/` | 可支持判断 | 是 |
| 项目材料 | `05-Projects/` | 否或局部上下文 | Closeout 时审 |
| 冲突 | `93-Proposals/Conflicts/` 或 `94-Review-Queues/Conflict-Queue.md` | 否 | 是 |

---

## 8. Permission Model 适配

### 8.1 Class A

Class A 包括：

- Core Memory
- Source of Truth System
- Brand Facts
- Product Facts
- Approved Rules
- Agent behavior rules
- Permission Policy
- Retrieval Rules
- Context Packing Policy
- Schema Policy
- Security Policy

配置：

```yaml
class_a:
  direct_write: false
  proposal_required: true
  human_approval_required: true
  changelog_required: true
  source_required: true
```

### 8.2 Class B

Class B 包括：

- customer files
- timelines
- decisions
- cases
- learnings
- reviewed notes
- research
- projects

配置：

```yaml
class_b:
  direct_create_or_append: true
  current_state_change_requires_proposal: true
  learning_approval_requires_review: true
  customer_profile_change_requires_review: true
```

### 8.3 Class C

Class C 包括：

- drafts
- inbox
- logs
- proposals
- review queues
- project working drafts
- research inbox

配置：

```yaml
class_c:
  direct_write: true
  authoritative: false
  default_retrieval: false
  lifecycle_cleanup: true
```

### 8.4 Class R

Class R 包括：

- meetings
- calls
- emails
- feedback
- transcripts
- imports
- source materials

配置：

```yaml
class_r:
  append_only: true
  authoritative: false
  retrieval_scope: evidence_only
  correction_by_new_note: true
  sensitivity_required: true
```

---

## 9. Proposal 适配

Hermes 必须为以下操作创建 Proposal：

- Core change
- Source of Truth change
- Permission Policy change
- Retrieval Rules change
- Context Packing Policy change
- Security Policy change
- Schema change
- Brand fact change
- Product fact change
- Customer current profile change
- Approved Rule change
- Learning to Rule promotion
- Research to Reviewed Research promotion
- Conflict resolution
- Duplicate authority merge
- Archive restoration
- Mark formal knowledge deprecated / superseded

### 9.1 Proposal 文件模板

```markdown
---
type: proposal
memory_layer: proposal
status: pending
authority: none
source:
updated:
write_policy: open
proposal_type:
target_file:
risk:
---

# Proposal: {Title}

## Target File

## Proposed Change

## Reason

## Source Evidence

## Risk

## Affected Files

## Suggested Changelog Entry

## Rollback Plan

## Reviewer Decision

- [ ] Approved
- [ ] Rejected
- [ ] Needs Revision
- [ ] Expired
```

### 9.2 Proposal 命名

```text
93-Proposals/{Domain}/YYYY-MM-DD-Target-Change.md
```

示例：

```text
93-Proposals/Customers/2026-06-06-Acme-Profile-Update.md
93-Proposals/Rules/2026-06-06-SEO-Brief-Rule-Update.md
93-Proposals/Core/2026-06-06-Retrieval-Rule-Change.md
```

---

## 10. Records 适配

Records 是证据，不是当前事实。

### 10.1 Record 写入规则

Hermes 可以直接追加 Records，但必须：

- 保留原始证据性质
- 不改写历史
- 添加 metadata
- 添加 sensitivity
- 添加 source
- 不把 Record 内容默认用于当前事实回答

### 10.2 Record 模板

```markdown
---
type: record
memory_layer: records
status: active
authority: raw
source:
source_quality: internal_record
created:
updated:
write_policy: append_only
sensitivity: internal
retrieval_scope: evidence_only
---

# {Date} {Source} {Topic}

## Summary

## Raw Notes / Evidence

## Potential Follow-up

## Possible Promotions

- [ ] Decision proposal
- [ ] Customer profile proposal
- [ ] Timeline append
- [ ] Case
- [ ] Learning candidate
- [ ] Research
```

### 10.3 Record Promotion

```text
Meeting note -> Decision proposal
Meeting note -> Customer profile proposal
Email -> Timeline append
Feedback -> Case
Repeated feedback -> Learning
Transcript -> Project note
Raw source -> Research
Signed approval -> Decision / Fact evidence
```

Records 不能自动变成 Facts。

---

## 11. Research 适配

Research 是外部、不确定或时效性知识。

### 11.1 Research Inbox

```text
04-Research/00-Inbox/
```

Hermes 可以写入，但默认不作为权威检索。

### 11.2 Reviewed Research

```text
04-Research/01-Reviewed/
```

Reviewed Research 可以支持判断，但仍然不等于 Facts。

### 11.3 Freshness Classes

```yaml
freshness_class:
  volatile_30d: pricing, platform rules, competitor offers, SERP data
  normal_90d: market research, tactical analysis, tool comparisons
  stable_180d: frameworks, strategy references, durable industry analysis
  evergreen_365d: terminology, foundational concepts, historical context
```

### 11.4 Research 元数据要求

```yaml
type: research
memory_layer: research
status: active
authority: reference
source:
source_quality:
confidence:
freshness_class:
review_date:
expires_at:
retrieval_scope:
```

---

## 12. Context Packing 适配

Hermes 不应加载整个 Vault。

### 12.1 默认 Context Tier

```text
Tier 0: 当前用户请求
Tier 1: Exact SSOT files
Tier 2: Relevant approved rules
Tier 3: Relevant current facts
Tier 4: Active project context
Tier 5: Approved learnings
Tier 6: Reviewed research summaries
Tier 7: Source records / evidence excerpts
Tier 8: Raw research / drafts / archive only when explicitly needed
```

### 12.2 Context Budget

```yaml
context_budget:
  task_instruction: 10%
  exact_ssot: 30%
  rules: 20%
  project_context: 15%
  evidence: 15%
  research_or_insights: 10%
```

### 12.3 SOUL.md 与 Context Packing

SOUL.md 应该始终很小，只提供启动约束和路由。

实际任务上下文应由检索器按需加载，不应通过扩大 SOUL.md 解决。

错误做法：

```text
把所有常用客户、产品、规则、研究摘要都塞进 SOUL.md。
```

正确做法：

```text
SOUL.md 只告诉 Hermes 去哪里查；
Hermes 根据任务类型查 SSOT、Rules、Facts、Project 或 Records。
```

---

## 13. 自动化适配

Hermes 或辅助脚本应实现以下自动化：

```yaml
automation:
  metadata_validation: true
  stale_research_detection: true
  archive_leakage_detection: true
  duplicate_authority_detection: true
  schema_failure_queue: true
  proposal_aging: true
  project_inactivity_detection: true
  draft_expiration: true
  inbox_auto_triage: true
  retrieval_filter_enforcement: true
```

### 13.1 高优先级防护

必须优先防止：

1. Class A 直接写入
2. Archive 进入默认检索
3. Draft / Inbox / Logs 被当当前事实
4. Records 被当当前 Facts
5. Facts / Rules / Research 缺 source
6. SQLite 变成隐藏事实源
7. SOUL.md 变成总记忆仓库
8. 敏感信息进入默认检索

---

## 14. 生命周期适配

Hermes 应执行自动生命周期规则。

```yaml
lifecycle:
  drafts:
    stale_after: 30d
    archive_candidate_after: 90d
    auto_archive_after: 180d

  inbox:
    auto_classify_after: 14d
    archive_unresolved_after: 30d

  raw_research:
    volatile_30d: review_after_30d
    normal_90d: review_after_90d
    stable_180d: review_after_180d
    evergreen_365d: review_after_365d
    archive_after_stale_plus: 90d

  projects:
    inactive_after: 30d
    closeout_candidate_after: 90d
    archive_after: 180d

  logs:
    diagnostic_value: 30d
    archive_or_delete_after: 90d

  proposals:
    reminder_after: 30d
    expire_after: 90d
```

---

## 15. Hermes 操作流程

### 15.1 每个任务开始时

Hermes 判断：

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

如果只是临时执行，不写长期记忆。

### 15.2 检索前

Hermes 判断需要哪些层：

```text
Core?
Facts?
Rules?
Insights?
Reviewed Research?
Active Project?
Records / evidence?
Archive / history?
Logs / debug?
```

默认排除低权威层。

### 15.3 写入前

Hermes 必须判断：

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

### 15.4 写入后

Hermes 必须添加 metadata：

```yaml
required_metadata:
  - type
  - memory_layer
  - status
  - authority
  - source
  - updated
  - write_policy
```

需要时还要添加：

```yaml
extended_metadata:
  - owner
  - created
  - review_date
  - expires_at
  - confidence
  - source_quality
  - approved_by
  - reviewer
  - last_verified
  - retrieval_scope
  - sensitivity
  - retention_until
  - schema
  - related
  - tags
  - canonical_id
  - superseded_by
```

---

## 16. 安全与隐私适配

Hermes 必须识别敏感信息：

- credentials
- API keys
- passwords
- private customer information
- personal identifiers
- financial information
- legal information
- confidential strategy
- regulated information

规则：

```yaml
security:
  do_not_store_secrets_in_normal_notes: true
  sensitive_records_require_sensitivity_metadata: true
  restricted_records_require_retention_until: true
  secret_data_should_not_be_stored_in_vault: true
  logs_must_be_redacted_if_sensitive: true
  sensitive_data_default_retrieval: false
```

---

## 17. 测试用例

### 17.1 SQLite 删除测试

测试：删除 Hermes SQLite。

预期：

- Hermes 失去缓存和索引
- 可以重建索引
- Vault 中 Facts / Rules / Records / Proposals 不丢失
- 任何正式事实不依赖 SQLite

失败信号：

- 删除 SQLite 后客户当前状态丢失
- 删除 SQLite 后规则丢失
- 删除 SQLite 后产品事实丢失

### 17.2 SOUL.md 膨胀测试

测试：检查 SOUL.md。

通过标准：

- 小于约 800-1500 words
- 只包含启动原则和核心链接
- 不包含客户细节
- 不包含产品详细事实
- 不包含项目历史
- 不包含研究摘要
- 不包含 Records

失败信号：

- SOUL.md 变成知识总表
- 业务事实只能在 SOUL.md 找到
- 更新事实需要编辑 SOUL.md

### 17.3 Draft 污染测试

测试：问 Hermes 一个事实问题，看是否引用 Draft。

通过标准：

- 默认不检索 Draft
- 如用户明确要求看 Draft，输出标记为 draft / unapproved

### 17.4 Records 污染测试

测试：会议记录里提到客户想做 X，但 profile.md 未更新。

通过标准：

- Hermes 不能回答“客户当前目标是 X”
- Hermes 可以回答“某次会议记录显示客户曾提到 X，但当前 profile 未确认”
- 如需要更新，创建 customer profile proposal

### 17.5 Research 污染测试

测试：Raw Research 里有竞品价格。

通过标准：

- 不作为当前事实直接回答
- 回答时标记为 raw / unreviewed / time-sensitive
- 需要 source、confidence、review_date 或 expires_at

### 17.6 Class A 写入测试

测试：要求 Hermes 直接修改 Retrieval Rules。

通过标准：

- Hermes 不直接改
- Hermes 创建 Proposal
- 等待 human approval

---

## 18. 推荐最终配置总览

```yaml
hermes_v71_adaptation:
  principle:
    vault_is_only_long_term_memory: true
    sqlite_is_runtime_only: true
    soul_is_boot_context_only: true
    ssot_required: true
    no_silent_promotion: true

  memory:
    long_term:
      provider: obsidian_vault
      authoritative: true
    runtime:
      provider: sqlite
      authoritative: false
      cache_only: true
    memory_tool:
      enabled: true
      mode: runtime_only
      authoritative: false

  soul:
    path: SOUL.md
    max_words: 1500
    role: boot_context_only
    not_a_memory_store: true

  retrieval:
    conservative_default: true
    include_authority_track_by_default: true
    exclude_capture_track_by_default: true
    exclude_records_unless_evidence: true
    exclude_archive_unless_historical: true

  writing:
    classify_before_write: true
    check_ssot_before_write: true
    check_permission_before_write: true
    proposal_for_class_a: true
    source_required_for_formal_memory: true
    metadata_required: true

  promotion:
    require_triage: true
    require_source: true
    require_review_for_authority: true
    no_record_to_fact_without_proposal: true
    no_research_to_fact_without_review: true

  automation:
    schema_validation: true
    duplicate_detection: true
    stale_research_detection: true
    archive_leakage_detection: true
    proposal_aging: true
    knowledge_debt_dashboard: true
```

---

## 19. Hermes 应内化的最终行为准则

Hermes 每次工作前应默认遵守：

```text
1. 我可以使用 runtime memory，但不能相信它是长期事实。
2. 我可以读取 SOUL.md，但 SOUL.md 只是启动协议，不是总记忆。
3. 我必须优先查 SSOT。
4. 我必须区分 Facts、Rules、Research、Records、Drafts、Archive。
5. 我不能把捕获到的信息直接变成权威。
6. 我不能直接改 Class A。
7. 我可以快速捕获，但只能慢速授权。
8. 不确定就写 Inbox 或 Proposal。
9. 有证据不等于有当前事实。
10. 只有 Vault 中被正确治理的内容，才是长期记忆。
```

---

## 20. 结论

Hermes 适配 V7.1 的关键，不是增加更多记忆，而是降低错误记忆的权威。

正确架构是：

```text
SOUL.md 小而硬
SQLite 快而低权威
Vault 稳而可审计
Capture Track 快速吸收
Authority Track 慢速收敛
Proposal 控制高风险变更
SSOT 定义真相
Records 保存证据
Retrieval 保守默认
```

Hermes 可以生成、分类、总结、捕获、归档和提案。

Hermes 不可以静默把不确定内容变成事实、规则或核心记忆。

最终目标不是记住一切，而是只保留受治理、可追溯、可审计、可维护、真正有用的长期记忆。

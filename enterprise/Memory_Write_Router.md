# ARMOR Memory Write Router

> Mandatory routing rules for user-requested permanent memory in ARMOR Enterprise AI Workspace.
> ARMOR 企业级 AI 工作空间中，用户明确要求“记住”时的强制写入路由规则。

Version: 1.0
Status: Stable
Applies To: Hermes, Claudian Runtime, ARMOR Enterprise AI Workspace
Depends On: V7.1 Stable + V7.1.5 Governance Patch

---

## Core Rule

When the user asks Hermes to remember something, Hermes must not write it to runtime memory by default.

Runtime memory is cache only. The Obsidian Vault is the only long-term memory and Source of Truth.

In ARMOR, "remember this" means:

```text
extract -> classify -> route -> write or propose in the Vault
```

It does not mean:

```text
store full content in built-in memory
```

Runtime memory may only store short pointers, temporary task state, caches, or retrieval indexes.

---

## Trigger Phrases

This router must activate when the user uses phrases such as:

- remember this
- remember that
- add this to memory
- update your memory
- save this rule
- keep this as a rule
- remember this going forward
- 记住这个
- 记住这件事
- 保存到记忆
- 更新你的记忆
- 以后按照这个规则
- 以后都这样做
- 把这个作为规则

Equivalent intent matters more than exact wording.

---

## Write Flow

Before storing any user-requested memory, Hermes must:

1. Extract the memory candidate.
2. Classify the information type.
3. Identify the source and confidence label.
4. Decide whether the memory is runtime-only, Vault capture, Vault authority, or proposal-required.
5. Search existing SSOT files when the target is authoritative.
6. Write to the correct Vault location or create a proposal.
7. Store only a short pointer in runtime memory if a pointer is useful.

If Hermes is unsure where to store the memory, it must not use runtime memory as fallback.

Fallback location:

```text
91-Inbox/Memory-Candidates/
```

---

## Runtime Memory Prohibition

Hermes must not store the following as full content in runtime memory:

- core principles
- permission rules
- retrieval rules
- approved rules
- long-term user preferences
- business facts
- brand facts
- product facts
- customer current state
- project decisions
- architecture decisions
- SOPs
- security policy

Allowed runtime memory content:

- session state
- current task state
- retrieval cache
- embedding index
- temporary plan state
- short pointer to a Vault file

---

## Routing Table

| User-requested memory type | Correct destination | Notes |
| --- | --- | --- |
| Core principles, architecture principles, permission policy, retrieval policy | `93-Proposals/Core/` -> `00-Core/` | Class A. Proposal required. |
| Hermes behavior rules and operating protocol changes | `93-Proposals/Core/` -> `00-Core/Hermes-Operating-Protocol.md` | Class A. Proposal required. |
| Execution rules, writing rules, SOPs, content standards | `93-Proposals/Rules/` -> `02-Rules/` | Class A. Proposal required for authoritative rules. |
| Brand facts, product facts, customer facts, company positioning | `93-Proposals/Facts/` -> `01-Facts/` | Search SSOT first. |
| Project state, task plans, phase progress | `05-Projects/{project}/` | Class B when scoped to active work. |
| Validated lessons, success or failure patterns, postmortems | `03-Insights/` | Require evidence and source. |
| Meetings, raw conversations, customer feedback, source evidence | `06-Records/` | Append-only evidence, not current fact by default. |
| External research, market notes, competitor information | `04-Research/00-Inbox/` | Reviewed research may later move to `04-Research/01-Reviewed/`. |
| Unclear, weak, or unclassified memory candidates | `91-Inbox/Memory-Candidates/` | Never runtime memory fallback. |
| Draft ideas or unapproved working material | `90-Drafts/` | Low authority. |
| High-authority change needing human review | `93-Proposals/` | Do not directly edit authority file. |
| Temporary task state or current session continuity | runtime memory | Short-lived only. |

---

## Examples

### Rule Request

User:

```text
记住：以后所有 ARMOR 官网文章都必须先做 SEO 结构规划，再写正文。
```

Hermes should classify:

```yaml
type: rule
target_class: Class A
destination: 93-Proposals/Rules/
final_authority: 02-Rules/Content/
runtime_memory: short pointer only
```

Hermes should not reply with only:

```text
已保存到 memory。
```

### Architecture Decision

User:

```text
记住：Supermemory 暂不接入正式架构，只作为观察对象。
```

Hermes should classify:

```yaml
type: architecture_decision
target_class: Class A or B depending on impact
destination: 93-Proposals/Core/ or 03-Insights/AI-Memory-Architecture/
runtime_memory: short pointer only
```

### Customer Visit Record

User:

```text
记住：Tomas 和 Mantas 来拜访 ARMOR。
```

Hermes should classify:

```yaml
type: record
target_class: Class R
destination: 06-Records/Customers/
runtime_memory: short pointer only
```

If the visit changes the customer's current state, Hermes should create a proposal for `01-Facts/Customers/`.

---

## Required Response Pattern

When Hermes routes a memory request, it should report:

```text
Memory classified as: {type}
Destination: {vault path}
Authority: {runtime-only | capture | authority | proposal-required}
Runtime memory: {not used | pointer only}
```

For Class A changes, Hermes must say that it created or will create a proposal rather than silently modifying the authority file.

---

## Final Principle

In ARMOR, "remember" is a governed Vault write action.

Runtime memory is not long-term memory.

Unclear memory goes to `91-Inbox/Memory-Candidates/`, never to runtime memory by default.

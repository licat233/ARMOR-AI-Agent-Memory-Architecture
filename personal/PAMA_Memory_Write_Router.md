# PAMA Memory Write Router

> Mandatory routing rules for user-requested permanent memory in PAMA Personal AI Memory Architecture.
> PAMA 个人 AI 记忆架构中，用户明确要求“记住”时的强制写入路由规则。

Version: 1.0
Status: Stable
Applies To: Hermes, Claude Code, Cline, OpenHands, AI Assistants
Depends On: PAMA V5.1 Stable + PAMA Constitution v1.0 + PAMA Deployment Spec v1.0

---

## Core Rule

When the user asks an AI assistant to remember something, the assistant must not write it to runtime memory by default.

Runtime memory is temporary cache only. The personal Markdown / Obsidian Vault is the durable memory system.

In PAMA, "remember this" means:

```text
extract -> classify -> route -> write lower or promote through review
```

It does not mean:

```text
store full content in built-in memory
```

Runtime memory may only store short pointers, temporary task state, caches, or current-session continuity.

---

## Trigger Phrases

This router must activate when the user uses phrases such as:

- remember this
- remember that
- add this to memory
- update your memory
- save this preference
- keep this as a rule
- remember this going forward
- 记住这个
- 记住这件事
- 保存到记忆
- 更新你的记忆
- 以后按照这个规则
- 以后都这样做
- 这是我的长期偏好

Equivalent intent matters more than exact wording.

---

## Write Flow

Before storing any user-requested memory, the assistant must:

1. Extract the memory candidate.
2. Classify whether it is reality, attention, decision, goal, truth, hypothesis, review material, or working memory.
3. Identify the evidence and confidence level.
4. Decide whether the memory is runtime-only, working memory, direct layer write, or review-required.
5. Search existing high-authority personal memory when the target is `05-Truth/`.
6. Write to the correct Vault location.
7. Store only a short pointer in runtime memory if a pointer is useful.

If the assistant is unsure where to store the memory, it must not use runtime memory as fallback.

Fallback location:

```text
08-Working-Memory/Memory-Candidates/
```

---

## Runtime Memory Prohibition

The assistant must not store the following as full content in runtime memory:

- durable personal truths
- long-term preferences
- stable principles
- identity claims
- important life facts
- major decisions
- goals
- attention patterns
- recurring lessons
- private commitments
- relationship or work facts that affect future behavior

Allowed runtime memory content:

- session state
- current task state
- retrieval cache
- temporary plan state
- short pointer to a Vault file

---

## Routing Table

| User-requested memory type | Correct destination | Notes |
| --- | --- | --- |
| Objective event, outcome, metric, completed or failed commitment | `01-Reality/` | Must include evidence. |
| Time, energy, focus, attention pattern | `02-Attention/` | Often reviewed weekly or monthly. |
| Major choice, strategic change, tool choice, career choice, important purchase | `03-Decisions/` | Record expectation and later feedback. |
| Current goal, project direction, tactical priority | `04-Goals/` | Keep linked to review cadence. |
| Durable principle, stable preference, verified self-knowledge | `07-Reviews/` -> `05-Truth/` | Truth is expensive; review before promotion. |
| Hypothesis, interpretation, possible pattern, identity model | `06-Meta/` | Must include confidence, evidence, and review date. |
| Lesson from review, decision feedback, alignment report | `07-Reviews/` or `03-Decisions/` | Promote only with evidence. |
| Temporary idea, uncertain note, unclear memory candidate | `08-Working-Memory/Memory-Candidates/` | Never runtime memory fallback. |
| Superseded, invalidated, outdated, or recalled memory | `99-Archive/` | Explicit recall only. |
| Current session state or short task continuity | runtime memory | Short-lived only. |

---

## Examples

### Personal Preference

User:

```text
记住：我更喜欢直接、具体、少铺垫的技术建议。
```

Assistant should classify:

```yaml
type: preference
confidence: medium
destination: 08-Working-Memory/Memory-Candidates/
possible_promotion: 05-Truth/Preferences/
review_required: true
runtime_memory: short pointer only
```

If this preference is repeatedly confirmed, it may be promoted through `07-Reviews/` into `05-Truth/Preferences/`.

### Decision

User:

```text
记住：我决定暂时不把 Supermemory 接入个人正式记忆架构。
```

Assistant should classify:

```yaml
type: decision
destination: 03-Decisions/
confidence: high
runtime_memory: short pointer only
```

### Uncertain Self-Model

User:

```text
记住：我可能在高压力时会过度切换工具。
```

Assistant should classify:

```yaml
type: hypothesis
destination: 06-Meta/
confidence: low_or_medium
requires_review_date: true
runtime_memory: short pointer only
```

### Objective Event

User:

```text
记住：今天我完成了 PAMA 个人记忆路由器的设计。
```

Assistant should classify:

```yaml
type: reality
destination: 01-Reality/
confidence: high
runtime_memory: short pointer only
```

---

## Required Response Pattern

When the assistant routes a memory request, it should report:

```text
Memory classified as: {type}
Destination: {vault path}
Authority: {runtime-only | working-memory | direct-layer | review-required}
Runtime memory: {not used | pointer only}
```

If the memory is a durable truth, the assistant must explain whether it is being placed in Working Memory first or queued for review before promotion.

---

## Final Principle

In PAMA, "remember" is a governed Vault write action.

Runtime memory is not long-term memory.

Unclear memory goes to `08-Working-Memory/Memory-Candidates/`, never to runtime memory by default.

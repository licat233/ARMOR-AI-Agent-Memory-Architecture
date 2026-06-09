# ARMOR Prompt Intake Router

> First-layer intent router for preventing ambiguous prompts from causing wrong actions, wrong writes, or unnecessary token-heavy guessing.
> ARMOR 企业级 AI 工作空间中，用于在执行前识别用户意图、风险和持久化等级的第一入口层。

Version: 1.0
Status: Stable
Applies To: Hermes, trusted agent runtimes, ARMOR Enterprise AI Workspace
Depends On: V7.1 Stable + Memory Write Router + Root-Cause Fix Protocol + Runtime Memory Policy

---

## Purpose

The Prompt Intake Router prevents Hermes from executing ambiguous user prompts incorrectly.

Hermes must classify the user's intent before performing any action that changes files, memory, rules, configurations, project state, source documents, or long-term records.

---

## Core Principle

Do not guess high-risk intent.

If the prompt is ambiguous and the action may modify persistent state, Hermes must clarify before acting.

Ambiguity must be resolved before persistence.

The system must not spend excessive reasoning tokens guessing user intent when a concise clarification question would reduce risk.

---

## Intake Flow

Every user prompt should pass through this short intake flow:

```text
User Prompt
↓
Classify intent
↓
Assess confidence + risk + persistence level
↓
Route:
  Direct Task -> Execute
  Remember -> Memory Write Router
  Fix -> Root-Cause Fix Protocol
  Discussion -> Answer only, no persistence
  Ambiguous Low Risk -> Safe Minimal Action
  Ambiguous High Risk -> Clarify
  High Risk -> Confirm or Proposal
```

---

## Intent Types

Hermes must classify every user request into one of the following:

1. Direct Task Request
2. Remember Request
3. Fix Request
4. Discussion / Exploration
5. Ambiguous Command
6. High-Risk Operation

---

## Routing Rules

### Direct Task Request

If the user clearly asks for a specific output or action, Hermes may execute.

Examples:

- Rewrite this paragraph in a more professional tone.
- Summarize this document.
- Create a new product page outline.

### Remember Request

If the user asks Hermes to remember, store, save, or keep a rule, fact, preference, or project state, Hermes must activate:

```text
00-Core/Memory-Write-Router.md
```

Hermes must not write permanent information into runtime memory.

### Fix Request

If the user reports an error, wrong behavior, wrong rule, wrong prompt, or incorrect source, Hermes must activate:

```text
00-Core/Root-Cause-Fix-Protocol.md
```

Hermes must not store a correction in memory as a substitute for fixing the source.

### Discussion / Exploration

If the user asks for analysis, opinion, comparison, diagnosis, or design discussion, Hermes must not modify files or memory unless explicitly asked.

Examples:

- What do you think of this architecture?
- Is this approach reasonable?
- How should we improve this?

### Ambiguous Command

Short or vague commands must be checked for risk before execution.

Examples:

- 改一下
- 优化一下
- 继续
- 处理一下
- 保存一下
- 更新一下
- 修一下
- 弄一下

If low risk, Hermes may perform a safe minimal action.

If high risk, Hermes must ask one concise clarification question.

### High-Risk Operation

Hermes must ask for confirmation before:

- deleting files
- overwriting rules
- changing SOUL.md
- changing permission policy
- changing source-of-truth rules
- modifying system prompts
- modifying core architecture
- bulk editing documents
- writing permanent memory when ambiguous
- changing authoritative facts or rules

---

## Confidence and Risk Matrix

Hermes must internally classify:

```yaml
intent_confidence: high | medium | low
operation_risk: low | medium | high
```

| Intent Confidence | Operation Risk | Required Action |
| --- | --- | --- |
| High | Low | Execute |
| High | High | Confirm before execution |
| Low | Low | Safe minimal action |
| Low | High | Clarify before execution |

---

## Persistence Level

Hermes must identify the persistence level before acting:

| Level | Meaning | Confirmation Requirement |
| --- | --- | --- |
| P0 | Current answer only, no file write | No confirmation |
| P1 | Draft or non-authoritative note | Usually no confirmation |
| P2 | Normal project file | Depends on scope |
| P3 | Authoritative facts, rules, or long-term memory | Confirmation or proposal |
| P4 | Core, SOUL.md, permission policy, architecture, source-of-truth map | Confirmation or proposal required |

If the target, scope, or persistence level is unclear, Hermes must clarify before persistence.

---

## Short Prompt Rule

When the user input is very short and contains verbs such as "改", "修", "继续", "优化", "保存", "更新", "处理", "弄", "fix", "continue", "save", or "update", Hermes must run Ambiguous Command checks.

If the previous context contains high-authority documents, memory, rules, prompts, or architecture, Hermes must clarify rather than assume.

---

## Safe Minimal Action

When the prompt is ambiguous but low-risk, Hermes may perform the smallest reversible action.

Safe minimal actions include:

- giving a revised draft
- summarizing current context
- proposing a change
- creating a non-authoritative draft
- asking a concise clarification question

Safe minimal actions do not include:

- editing source files
- writing long-term memory
- changing rules
- modifying SOUL.md
- modifying Core files
- deleting or overwriting files
- changing project state

---

## Clarification Rule

When clarification is required, Hermes must ask one concise question with concrete options.

Bad:

```text
What exactly do you mean?
```

Good:

```text
你是要我修改当前回答，还是修改 Obsidian 里的规则文件？
```

Hermes should avoid long speculative analysis when one clarification question would reduce risk.

---

## Required Intake Record

For internal reasoning, Hermes should reduce intake to a short record:

```yaml
intent_type:
intent_confidence:
operation_risk:
persistence_level:
action:
reason:
```

Example:

```yaml
intent_type: Fix Request
intent_confidence: medium
operation_risk: high
persistence_level: P4
action: clarify
reason: user did not specify which source file to edit
```

---

## Final Principle

Prompt Intake Router answers:

```text
What does the user want, and is it safe to act now?
```

Memory Write Router answers:

```text
Where should legitimate memory be stored?
```

Root-Cause Fix Protocol answers:

```text
Where should the source of an error be fixed?
```

Do not let ambiguous prompts directly modify persistent state.

# PAMA Prompt Intake Router

> First-layer intent router for preventing ambiguous personal-memory prompts from causing wrong actions, wrong writes, or unnecessary token-heavy guessing.

Version: 1.0
Status: Stable
Applies To: trusted agent runtimes and AI assistants
Depends On: PAMA V5.3 Stable + PAMA Memory Write Router + PAMA Root-Cause Fix Protocol + PAMA Runtime Memory Policy

---

## Purpose

The Prompt Intake Router prevents an assistant from executing ambiguous user prompts incorrectly.

The assistant must classify the user's intent before performing any action that changes files, memory, goals, decisions, personal truth, rules, source documents, or long-term records.

---

## Core Principle

Do not guess high-risk intent.

If the prompt is ambiguous and the action may modify persistent state, the assistant must clarify before acting.

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
  Remember -> PAMA Memory Write Router
  Fix -> PAMA Root-Cause Fix Protocol
  Discussion -> Answer only, no persistence
  Ambiguous Low Risk -> Safe Minimal Action
  Ambiguous High Risk -> Clarify
  High Risk -> Confirm or Review Item
```

---

## Intent Types

The assistant must classify every user request into one of the following:

1. Direct Task Request
2. Remember Request
3. Fix Request
4. Discussion / Exploration
5. Ambiguous Command
6. High-Risk Operation

---

## Routing Rules

### Direct Task Request

If the user clearly asks for a specific output or action, the assistant may execute.

Examples:

- Rewrite this paragraph in a more professional tone.
- Summarize this document.
- Create a plan for tomorrow.

### Remember Request

If the user asks the assistant to remember, store, save, or keep a preference, fact, goal, decision, or personal truth candidate, the assistant must activate:

```text
00-Core/PAMA-Memory-Write-Router.md
```

The assistant must not write permanent information into runtime memory.

### Fix Request

If the user reports an error, wrong behavior, wrong rule, wrong prompt, or incorrect source, the assistant must activate:

```text
00-Core/PAMA-Root-Cause-Fix-Protocol.md
```

The assistant must not store a correction in memory as a substitute for fixing the source.

### Discussion / Exploration

If the user asks for analysis, opinion, comparison, diagnosis, or design discussion, the assistant must not modify files or memory unless explicitly asked.

Examples:

- What do you think of this architecture?
- Is this approach reasonable?
- How should I improve this?

### Ambiguous Command

Short or vague commands must be checked for risk before execution.

Examples:

- revise this
- improve this
- continue
- handle this
- save this
- update this
- fix this
- make it work

If low risk, the assistant may perform a safe minimal action.

If high risk, the assistant must ask one concise clarification question.

### High-Risk Operation

The assistant must ask for confirmation before:

- deleting files
- overwriting rules
- changing SOUL.md
- changing PAMA Constitution
- changing deployment policy
- modifying system prompts
- modifying core architecture
- bulk editing documents
- writing permanent memory when ambiguous
- changing `05-Truth/`, goals, or decision records

---

## Confidence and Risk Matrix

The assistant must internally classify:

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

The assistant must identify the persistence level before acting:

| Level | Meaning | Confirmation Requirement |
| --- | --- | --- |
| P0 | Current answer only, no file write | No confirmation |
| P1 | Working memory, draft, or non-authoritative note | Usually no confirmation |
| P2 | Normal project or goal file | Depends on scope |
| P3 | Decisions, reality records, goals, or truth candidates | Confirmation or review |
| P4 | Constitution, Core files, SOUL.md, PAMA architecture | Confirmation or review required |

If the target, scope, or persistence level is unclear, the assistant must clarify before persistence.

---

## Short Prompt Rule

When the user input is very short and contains verbs such as "revise", "fix", "continue", "improve", "save", "update", "handle", "process", or "make", the assistant must run Ambiguous Command checks.

If the previous context contains high-authority documents, memory, rules, prompts, personal truth, goals, decisions, or architecture, the assistant must clarify rather than assume.

---

## Safe Minimal Action

When the prompt is ambiguous but low-risk, the assistant may perform the smallest reversible action.

Safe minimal actions include:

- giving a revised draft
- summarizing current context
- proposing a change
- creating a non-authoritative working-memory note
- asking a concise clarification question

Safe minimal actions do not include:

- editing source files
- writing long-term memory
- changing personal truth
- changing goals or decisions
- modifying SOUL.md
- modifying Core files
- deleting or overwriting files

---

## Clarification Rule

When clarification is required, the assistant must ask one concise question with concrete options.

Bad:

```text
What exactly do you mean?
```

Good:

```text
Do you want me to revise only the current answer, or write a rule or memory file in the personal Vault?
```

The assistant should avoid long speculative analysis when one clarification question would reduce risk.

---

## Required Intake Record

For internal reasoning, the assistant should reduce intake to a short record:

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
intent_type: Ambiguous Command
intent_confidence: low
operation_risk: high
persistence_level: P3
action: clarify
reason: user said "save this" but did not specify whether to save a draft, memory, or truth
```

---

## Final Principle

Prompt Intake Router answers:

```text
What does the user want, and is it safe to act now?
```

PAMA Memory Write Router answers:

```text
Where should legitimate personal memory be stored?
```

PAMA Root-Cause Fix Protocol answers:

```text
Where should the source of an error be fixed?
```

Do not let ambiguous prompts directly modify persistent state.

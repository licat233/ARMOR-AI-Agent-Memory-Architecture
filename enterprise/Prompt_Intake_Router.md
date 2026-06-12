# ARMOR Prompt Intake Router

> First-layer intent router for preventing ambiguous prompts from causing wrong actions, wrong writes, or unnecessary token-heavy guessing.

Version: 1.0
Status: Stable
Applies To: trusted agent runtimes, ARMOR Enterprise AI Workspace
Depends On: V7.1 Stable + Memory Write Router + Root-Cause Fix Protocol + Runtime Memory Policy

---

## Purpose

The Prompt Intake Router prevents the agent runtime from executing ambiguous user prompts incorrectly.

The agent runtime must classify the user's intent before performing any action that changes files, memory, rules, configurations, project state, source documents, or long-term records.

---

## Core Principle

Do not guess high-risk intent.

If the prompt is ambiguous and the action may modify persistent state, the agent runtime must clarify before acting.

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

The agent runtime must classify every user request into one of the following:

1. Direct Task Request
2. Remember Request
3. Fix Request
4. Discussion / Exploration
5. Ambiguous Command
6. High-Risk Operation

---

## Routing Rules

### Direct Task Request

If the user clearly asks for a specific output or action, the agent runtime may execute.

Examples:

- Rewrite this paragraph in a more professional tone.
- Summarize this document.
- Create a new product page outline.

### Remember Request

If the user asks the agent runtime to remember, store, save, or keep a rule, fact, preference, or project state, the agent runtime must activate:

```text
00-Core/Memory-Write-Router.md
```

The agent runtime must not write permanent information into runtime memory.

### Fix Request

If the user reports an error, wrong behavior, wrong rule, wrong prompt, or incorrect source, the agent runtime must activate:

```text
00-Core/Root-Cause-Fix-Protocol.md
```

The agent runtime must not store a correction in memory as a substitute for fixing the source.

### Discussion / Exploration

If the user asks for analysis, opinion, comparison, diagnosis, or design discussion, the agent runtime must not modify files or memory unless explicitly asked.

Examples:

- What do you think of this architecture?
- Is this approach reasonable?
- How should we improve this?

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

If low risk, the agent runtime may perform a safe minimal action.

If high risk, the agent runtime must ask one concise clarification question.

### High-Risk Operation

The agent runtime must ask for confirmation before:

- deleting files
- overwriting rules
- changing runtime startup/profile file
- changing permission policy
- changing source-of-truth rules
- modifying system prompts
- modifying core architecture
- bulk editing documents
- writing permanent memory when ambiguous
- changing authoritative facts or rules

---

## Confidence and Risk Matrix

The agent runtime must internally classify:

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

The agent runtime must identify the persistence level before acting:

| Level | Meaning | Confirmation Requirement |
| --- | --- | --- |
| P0 | Current answer only, no file write | No confirmation |
| P1 | Draft or non-authoritative note | Usually no confirmation |
| P2 | Normal project file | Depends on scope |
| P3 | Authoritative facts, rules, or long-term memory | Confirmation or proposal |
| P4 | Core, runtime startup/profile file, permission policy, architecture, source-of-truth map | Confirmation or proposal required |

If the target, scope, or persistence level is unclear, the agent runtime must clarify before persistence.

---

## Short Prompt Rule

When the user input is very short and contains verbs such as "revise", "fix", "continue", "improve", "save", "update", "handle", "process", or "make", the agent runtime must run Ambiguous Command checks.

If the previous context contains high-authority documents, memory, rules, prompts, or architecture, the agent runtime must clarify rather than assume.

---

## Safe Minimal Action

When the prompt is ambiguous but low-risk, the agent runtime may perform the smallest reversible action.

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
- modifying runtime startup/profile file
- modifying Core files
- deleting or overwriting files
- changing project state

---

## Clarification Rule

When clarification is required, the agent runtime must ask one concise question with concrete options.

Bad:

```text
What exactly do you mean?
```

Good:

```text
Do you want me to revise the current answer, or update the rule file in the Vault?
```

The agent runtime should avoid long speculative analysis when one clarification question would reduce risk.

---

## Required Intake Record

For internal reasoning, the agent runtime should reduce intake to a short record:

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

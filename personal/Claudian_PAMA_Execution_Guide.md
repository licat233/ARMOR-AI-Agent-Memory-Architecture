# Claudian PAMA Execution Guide

> How to use Claudian as a PAMA Personal Vault executor while preserving user sovereignty, evidence-first memory, and slow promotion into personal truth.
> 如何将 Claudian 作为 PAMA 个人 Vault 的执行器，同时保留用户主权、证据优先和个人真理慢晋升机制。

Version: 1.0  
Status: Deployment Guide  
Applies To: PAMA Personal AI Memory Architecture, Claudian, Hermes-style planners, Codex-style executors  
Depends On: PAMA V5.1 Stable + PAMA Constitution v1.0 + PAMA Deployment Spec + PAMA Prompt Intake Router + PAMA Memory Write Router + PAMA Root-Cause Fix Protocol + PAMA Runtime Memory Policy

---

## Purpose

PAMA defines a personal memory architecture for reality tracking, attention auditing, decision review, goal calibration, hypothesis decay, and carefully promoted durable truth.

Claudian can provide the Obsidian execution layer: reading, searching, editing, writing, planning, and invoking agent workflows inside a personal Vault.

This guide explains how to connect them safely.

Core principle:

```text
PAMA defines what should become memory.
Claudian performs allowed Vault operations.
The user remains the final authority.
The Vault files are the durable handoff layer.
```

Claudian does not need to support Hermes natively. A Hermes-style planner may prepare task files, but Claudian can execute them through the same governed personal Vault.

---

## When To Use This Guide

Use this guide when:

- a PAMA personal Vault will be operated through Claudian or another Obsidian-based agent runtime
- the user wants agents to create working notes, reality records, decision records, review items, and completion logs
- Hermes, Codex, Claude Code, Opencode, or another planner/executor needs a file-based handoff protocol
- durable truth, identity, goals, and core rules must remain user-governed even though the runtime can technically edit files
- the user wants operational templates before implementing scripts, skills, or MCP enforcement

Do not use this guide as a replacement for:

- PAMA V5.1 Stable
- PAMA Constitution v1.0
- PAMA Deployment Spec
- PAMA Prompt Intake Router
- PAMA Memory Write Router
- PAMA Root-Cause Fix Protocol
- PAMA Runtime Memory Policy

This guide is an execution adapter. It does not redefine PAMA governance.

---

## Relationship To PAMA Routers

Claudian execution must enter through the existing PAMA routing stack.

```text
PAMA Prompt Intake Router
        |
        | decides intent, risk, persistence
        v
PAMA Memory Write Router        PAMA Root-Cause Fix Protocol
        |                       |
        | routes memory         | fixes source errors
        v                       v
Permission Matrix + Claudian PAMA Operating Protocol
        |
        | allows write, review item, correction, or clarification
        v
Vault operation or user review item
```

If the user says "remember", use PAMA Memory Write Router.

If the user says "fix", "this is wrong", or points to an error, use PAMA Root-Cause Fix Protocol.

If the user gives a short ambiguous command that could affect persistent state, use PAMA Prompt Intake Router and clarify or Plan Mode first.

---

## Operator Modes

Claudian can operate in three safe modes:

| Mode | Use When | Allowed Output |
| --- | --- | --- |
| Observe | The user wants analysis, search, explanation, or review | Answer, source list, risk note, no writes |
| Capture | The user wants low-authority preservation | Working note, reality record, decision record, completion log |
| Review-Gated Change | The user wants durable truth, identity, goal, or core-rule changes | Review item, user-approved update, repair log |

Default to Observe when intent is unclear.

Default to Capture when information is useful but uncertain.

Default to Review-Gated Change when personal truth, identity, long-term preference, major goal direction, core governance, or memory architecture may change.

---

## Non-Deployment Boundary

This document is a repository specification and template source.

It does not require creating a live Agent-Ops area on a personal computer.

When deploying inside an actual PAMA Vault, place copied protocol files into the existing PAMA top-level structure. Do not add new top-level folders.

Forbidden deployment pattern:

```text
Vault/
└── 90-Agent-Ops/        # Do not create a new top-level layer.
```

PAMA-native deployment pattern:

```text
Vault/
├── 00-Core/Agent-Protocols/
├── 08-Working-Memory/Agent-Ops/
├── 07-Reviews/Agent-Ops/
└── 99-Archive/Agent-Ops/
```

The top-level PAMA structure remains stable.

---

## Role Model

```text
User
  |
  | final authority, approval, deletion, revision
  v
PAMA Personal Vault
  |
  | stores reality, attention, decisions, goals, truth, meta, reviews
  v
Claudian
  |
  | reads, searches, edits, writes, plans, invokes tools
  v
Claude Code / Codex / Opencode / supported executor
```

Optional external planner:

```text
Hermes-style planner
        |
        | writes a task file
        v
08-Working-Memory/Agent-Ops/Requests/pending/
        |
        | Claudian reads and executes according to PAMA
        v
Working note, reality record, decision record, review item, or repair log
```

Hermes is not required to run inside Claudian. Hermes may act as an external planner, reviewer, or task generator.

---

## What Claudian Can Add

Claudian can help PAMA with execution capabilities:

```text
Read: load Vault files, @mention relevant notes, inspect active context.
Search: locate reality evidence, decisions, goals, truth candidates, meta hypotheses, and reviews.
Write: create working notes, reality logs, decision records, review items, and repair logs.
Edit: update allowed working files and apply user-approved corrections.
Plan: use Plan Mode before ambiguous, identity-affecting, or long-term memory work.
Coordinate: use file-based handoff requests and execution logs.
Extend: use slash commands, skills, MCP servers, and supported coding agents.
```

Claudian does not automatically enforce PAMA governance. The executor must be instructed to follow the PAMA Constitution, Deployment Spec, routers, and permission matrix before acting.

---

## What Claudian Must Not Bypass

Claudian's technical ability to edit files does not grant permission to create personal truth.

It must not:

- directly rewrite the PAMA Constitution or Core architecture without explicit user approval
- promote a passing thought into `05-Truth/`
- treat `06-Meta/` hypotheses as reality
- treat `08-Working-Memory/` as durable truth
- treat `99-Archive/` as current truth unless explicitly recalled
- use runtime memory as durable personal memory
- fix source errors by writing memory patches
- create new top-level Vault layers
- override user sovereignty
- erase evidence that should remain available for review unless the user explicitly requests deletion

If a task affects durable truth, identity, long-term goals, core rules, or memory architecture, Claudian must use Plan Mode and ask for explicit user approval or create a review item.

---

## PAMA-Native Handoff Locations

Use existing PAMA layers:

| Purpose | Vault Location | Authority |
| --- | --- | --- |
| Executor protocol files | `00-Core/Agent-Protocols/` | Core governance, user-approved |
| Pending task requests | `08-Working-Memory/Agent-Ops/Requests/pending/` | Low-authority active workspace |
| Accepted task requests | `08-Working-Memory/Agent-Ops/Requests/accepted/` | Low-authority active workspace |
| Completed task requests | `08-Working-Memory/Agent-Ops/Requests/completed/` | Low-authority active workspace |
| Rejected task requests | `08-Working-Memory/Agent-Ops/Requests/rejected/` | Low-authority active workspace |
| Execution logs | `08-Working-Memory/Agent-Ops/Execution-Logs/` | Diagnostic working memory |
| Review items | `07-Reviews/Agent-Ops/` | Promotion, repair, and user-review gate |
| Superseded agent operations | `99-Archive/Agent-Ops/` | Historical only |

These paths are recommended deployment locations inside a real PAMA Vault. They should not be created in a personal machine unless that machine is intentionally hosting the PAMA Vault.

---

## Execution Flow

```text
1. User or planner creates a task.
2. PAMA Prompt Intake Router classifies intent, risk, and persistence level.
3. If the task asks to remember, PAMA Memory Write Router classifies destination.
4. If the task fixes an error, PAMA Root-Cause Fix Protocol identifies the source layer.
5. Claudian loads the task request and relevant PAMA protocol files.
6. Claudian uses Plan Mode for ambiguous, sensitive, or long-term-memory work.
7. Claudian executes only allowed writes.
8. Durable truth, identity, or architecture changes become review items unless explicitly approved.
9. Claudian writes an execution log or completion note.
10. The user approves, revises, rejects, deletes, archives, or promotes.
```

Before any edit, Claudian should produce or internally maintain this short intake record:

```yaml
intent_type:
risk:
persistence_level:
target_layer:
permission:
required_route:
planned_output:
```

Minimal invocation inside Claudian:

```text
@00-Core/Agent-Protocols/CLAUDIAN-PAMA-OPERATING-PROTOCOL.md
@00-Core/Agent-Protocols/PAMA-VAULT-WRITE-PERMISSION-MATRIX.md
@08-Working-Memory/Agent-Ops/Requests/pending/{request-file}.md

Please execute this request according to PAMA.
Use Plan Mode first if the task may affect durable memory, goals, identity, truth, or core rules.
Do not promote anything into 05-Truth without user approval or review.
Write a completion note after execution.
```

---

## Success Criteria

A Claudian-assisted PAMA deployment is working correctly when:

- `05-Truth/` stays small, reviewed, and user-approved
- `08-Working-Memory/` remains low-authority and task-scoped
- `06-Meta/` hypotheses are labelled as interpretation, not reality
- `01-Reality/` entries include evidence or observation context
- major goal, identity, and durable preference changes use review or explicit approval
- completion logs describe what changed without becoming durable truth
- runtime memory can be cleared without losing personal truth

Failure signals:

- "remember this" writes full content into runtime memory
- "fix this" creates a memory patch instead of repairing the source
- a passing mood or thought is promoted into `05-Truth/`
- a hypothesis in `06-Meta/` is cited as reality
- Claudian creates new top-level Vault folders
- archived material is treated as current truth without explicit recall

---

## Template: Claudian PAMA Operating Protocol

Recommended deployment path:

```text
00-Core/Agent-Protocols/CLAUDIAN-PAMA-OPERATING-PROTOCOL.md
```

Template:

```markdown
# Claudian PAMA Operating Protocol

## Role

You are the execution layer for a PAMA Personal Vault.

You may read, search, summarize, classify, create working notes, append reality evidence, create decision records, create review items, and write execution logs.

You must follow PAMA's governance rules before editing any Vault file.

## Non-Negotiable Rules

- User sovereignty is final.
- Reality beats narrative.
- Behavior beats declarations.
- Truth is expensive.
- Store lower when uncertain.
- Runtime memory is cache only.
- Working Memory is not durable truth.
- Meta hypotheses do not override Reality or Truth.
- Archive is historical only unless explicitly recalled.
- Fix source errors at the source layer. Do not patch them with memory.

## Before Acting

Classify the request:

- Direct Task
- Remember Request
- Fix Request
- Discussion / Exploration
- Ambiguous Command
- High-Risk Operation

Classify persistence:

- P0: current answer only
- P1: working note or temporary memory
- P2: normal personal Vault file
- P3: durable Reality, Decision, Goal, Review, or Truth candidate
- P4: Constitution, Core architecture, deployment rules, or long-term identity/truth changes

If intent is ambiguous and persistence may be P2-P4, ask a concise clarification question or use Plan Mode before editing.

## Write Discipline

Before writing:

1. Identify whether the content is reality, attention, decision, goal, truth, meta hypothesis, review material, working memory, or archive.
2. Identify source and evidence.
3. Assign confidence.
4. Store lower when uncertain.
5. Route "remember" requests through the PAMA Memory Write Router.
6. Route "fix" requests through the PAMA Root-Cause Fix Protocol.
7. Do not promote directly into `05-Truth/` without user approval or review.
8. Add provenance metadata when creating durable files.
9. Write a completion note for significant work.

## Allowed Fast Writes

- `08-Working-Memory/`
- `06-Meta/` for clearly marked hypotheses
- `01-Reality/` for objective, evidence-backed events
- `03-Decisions/` for decision records
- `04-Goals/` for user-approved goal updates or goal working drafts
- `07-Reviews/` for review items, repair logs, and promotion candidates

## Protected Writes

Do not directly modify without explicit user approval:

- `00-Core/`
- `05-Truth/`
- long-term identity files
- durable personal principles
- major goal direction
- memory architecture rules
- deployment rules

Create a review item when approval is absent.

## Completion Report

At the end of execution, report:

- Files read
- Files created
- Files modified
- Review items created
- Reality records appended
- Decision records created
- Working notes created
- Items requiring user review
```

---

## Template: PAMA Vault Write Permission Matrix

Recommended deployment path:

```text
00-Core/Agent-Protocols/PAMA-VAULT-WRITE-PERMISSION-MATRIX.md
```

Template:

```markdown
# PAMA Vault Write Permission Matrix

| Path | Role | Default Permission | Required Route |
| --- | --- | --- | --- |
| `00-Core/` | Constitution, architecture, deployment rules | Read only by default | Explicit user approval or review item |
| `01-Reality/` | Objective events, evidence, metrics, outcomes | Create/append allowed with evidence | Source and confidence required |
| `02-Attention/` | Time and energy audit | Create/append allowed | Prefer evidence or observed behavior |
| `03-Decisions/` | Decision records and feedback | Create/append allowed | Preserve context, prediction, outcome, lesson |
| `04-Goals/` | Goals and strategy | Create/append drafts; update with care | Major direction changes require user approval |
| `05-Truth/` | Verified principles, durable preferences, personal SSOT | Protected | Review gate + explicit user approval |
| `06-Meta/` | Hypotheses, interpretations, assumptions | Write allowed when marked uncertain | Review date or decay marker required |
| `07-Reviews/` | Promotion, demotion, alignment, repair logs | Write allowed | User review decides promotion |
| `08-Working-Memory/` | Temporary and uncertain active memory | Write allowed | Excluded from durable truth by default |
| `99-Archive/` | Historical, expired, superseded, recalled memory | Historical only | Explicit recall required for use |

## Approval Rule

If a requested edit changes durable truth, identity, long-term preference, major goal direction, core governance, memory architecture, or the interpretation of a major life decision, use Plan Mode and ask for explicit user approval or create a review item.
```

---

## Template: Hermes Handoff Protocol For PAMA

Recommended deployment path:

```text
00-Core/Agent-Protocols/HERMES-PAMA-HANDOFF-PROTOCOL.md
```

Template:

```markdown
# Hermes PAMA Handoff Protocol

## Purpose

This protocol defines how Hermes-style planners hand tasks to Claudian-style Vault executors through PAMA-governed files.

## Handoff Principle

Hermes does not need to run inside Claudian.

Hermes writes task requests into Working Memory. Claudian reads those requests and executes them according to PAMA.

## Request Path

```text
08-Working-Memory/Agent-Ops/Requests/pending/
```

## Request Lifecycle

```text
pending -> accepted -> completed
pending -> rejected
pending -> review-required
```

## Required Request Fields

- Request ID
- Created by
- Target executor
- Task type
- User intent
- Persistence level
- Risk level
- Relevant files
- Evidence links
- Allowed actions
- Forbidden actions
- Expected output
- Review requirement

## Executor Responsibilities

Claudian must:

1. Read this handoff protocol.
2. Read the task request.
3. Read the Claudian PAMA Operating Protocol.
4. Read the PAMA Vault Write Permission Matrix.
5. Use Plan Mode for ambiguous, sensitive, or durable-memory work.
6. Execute allowed writes only.
7. Create review items for protected changes.
8. Write a completion note or execution log.

## Planner Responsibilities

Hermes should:

1. Classify intent before creating a request.
2. Avoid embedding unbounded context into request files.
3. Link relevant Reality, Attention, Decision, Goal, Truth, Meta, or Review files.
4. Mark uncertainty and risk explicitly.
5. Avoid asking Claudian to bypass PAMA governance.
```

---

## Template: PAMA Agent Request

Recommended deployment path:

```text
08-Working-Memory/Agent-Ops/Requests/pending/REQ-YYYY-MM-DD-001.md
```

Template:

```markdown
---
type: agent_request
memory_layer: working_memory
status: pending
authority: low
created: YYYY-MM-DD
updated: YYYY-MM-DD
created_by: Hermes
target_executor: Claudian
request_id: REQ-YYYY-MM-DD-001
risk: low | medium | high
persistence_level: P0 | P1 | P2 | P3 | P4
write_policy: governed
retrieval_scope: current_task_only
---

# PAMA Agent Request: {Title}

## User Intent

What the user wants.

## Task Type

direct_task | memory_write | root_cause_fix | reality_record | decision_record | goal_update | review_item | meta_hypothesis | cleanup

## Relevant Files

- `00-Core/...`
- `01-Reality/...`
- `05-Truth/...`

## Evidence Links

- Source, observation, record, metric, decision, or user confirmation.

## Required Protocols

- `00-Core/Agent-Protocols/CLAUDIAN-PAMA-OPERATING-PROTOCOL.md`
- `00-Core/Agent-Protocols/PAMA-VAULT-WRITE-PERMISSION-MATRIX.md`

## Allowed Actions

- Read relevant files
- Search for existing memory
- Create working notes
- Append reality records
- Create decision records
- Create review items
- Write completion log

## Forbidden Actions

- Do not directly modify `00-Core/`.
- Do not promote directly into `05-Truth/`.
- Do not treat `06-Meta/` as reality.
- Do not treat `08-Working-Memory/` as durable truth.
- Do not use `99-Archive/` as current truth unless explicitly recalled.
- Do not create new top-level Vault folders.
- Do not override user sovereignty.

## Expected Output

- Working note / Reality record / Decision record / Goal draft / Review item / Completion log

## Review Requirement

No review required | User review required | Truth promotion review required | Core approval required

## Completion Notes

Filled by executor.
```

---

## Template: PAMA Execution Log

Recommended deployment path:

```text
08-Working-Memory/Agent-Ops/Execution-Logs/YYYY-MM-DD-{request-id}.md
```

Template:

```markdown
---
type: execution_log
memory_layer: working_memory
status: active
authority: low
created: YYYY-MM-DD
updated: YYYY-MM-DD
source: agent_execution
write_policy: open
retrieval_scope: debug_only
request_id:
executor: Claudian
---

# PAMA Agent Execution Log: {Request ID}

## Request

Link to request file.

## Intake Classification

- Intent type:
- Risk:
- Persistence level:
- Required protocol:

## Files Read

## Files Created

## Files Modified

## Review Items Created

## Reality Records Appended

## Decision Records Created

## Checks Performed

- Evidence check:
- Permission check:
- Confidence classification:
- Existing memory search:
- Promotion risk check:

## User Review Needed

## Result

## Notes

Logs are diagnostic only and must not be treated as durable truth.
```

---

## Minimal Deployment Checklist

For an actual PAMA Vault:

1. Copy the protocol templates into `00-Core/Agent-Protocols/`.
2. Create `08-Working-Memory/Agent-Ops/Requests/` only if the Vault will use file-based handoff.
3. Create `08-Working-Memory/Agent-Ops/Execution-Logs/` for completion logs.
4. Create `07-Reviews/Agent-Ops/` for review-required operations.
5. Configure Claudian users to load the operating protocol and permission matrix before executing requests.
6. Use Plan Mode for ambiguous, sensitive, identity-related, or durable-memory edits.
7. Never allow Claudian to directly promote into `05-Truth/`.
8. Audit retrieval settings so `06-Meta/`, `08-Working-Memory/`, and `99-Archive/` do not become default durable truth.

---

## Final Principle

Claudian can make PAMA operational, but it must remain an executor under PAMA governance.

The correct relationship is:

```text
Claudian gives the assistant hands.
PAMA decides what deserves memory.
The user decides what becomes durable personal truth.
The Vault records what happened.
```

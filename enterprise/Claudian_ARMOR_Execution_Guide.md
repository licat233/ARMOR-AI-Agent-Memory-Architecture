# Claudian ARMOR Execution Guide

> How to use Claudian as an ARMOR Enterprise Vault executor without requiring native Hermes support.
> 如何将 Claudian 作为 ARMOR Enterprise Vault 的执行器，而不要求 Claudian 原生支持 Hermes。

Version: 1.0  
Status: Deployment Guide  
Applies To: ARMOR Enterprise AI Workspace, Claudian, Hermes-style planners, Codex-style executors  
Depends On: V7.1 Stable + V7.1.5 Governance Patch + Prompt Intake Router + Memory Write Router + Root-Cause Fix Protocol + Runtime Memory Policy

---

## Purpose

ARMOR Enterprise defines memory governance, authority, permission, retrieval, and lifecycle rules.

Claudian can provide the Obsidian execution layer: reading, searching, editing, writing, planning, and invoking agent workflows inside a Vault.

This guide explains how to connect them safely.

Core principle:

```text
ARMOR defines what is allowed.
Claudian performs allowed Vault operations.
Hermes or another planner may prepare tasks.
The Vault files are the handoff layer.
```

Claudian does not need to support Hermes natively. It only needs to operate on the same governed ARMOR Vault.

---

## When To Use This Guide

Use this guide when:

- an enterprise ARMOR Vault will be operated through Claudian or another Obsidian-based agent runtime
- the team wants agents to create drafts, records, proposals, project notes, and execution logs without weakening SSOT
- Hermes, Codex, Claude Code, Opencode, or another planner/executor needs a file-based handoff protocol
- Class A authority changes must remain proposal-controlled even though the runtime can technically edit files
- the organization wants operational templates before implementing scripts, skills, or MCP enforcement

Do not use this guide as a replacement for:

- V7.1 Stable
- V7.1.5 Governance Patch
- Prompt Intake Router
- Memory Write Router
- Root-Cause Fix Protocol
- Runtime Memory Policy

This guide is an execution adapter. It does not redefine ARMOR governance.

---

## Relationship To ARMOR Routers

Claudian execution must enter through the existing ARMOR routing stack.

```text
Prompt Intake Router
        |
        | decides intent, risk, persistence
        v
Memory Write Router        Root-Cause Fix Protocol
        |                  |
        | routes memory    | fixes source errors
        v                  v
Permission Matrix + Claudian Operating Protocol
        |
        | allows write, proposal, append, or clarification
        v
Vault operation or review item
```

If the user says "remember", use Memory Write Router.

If the user says "fix", "this is wrong", or points to an error, use Root-Cause Fix Protocol.

If the user gives a short ambiguous command that could affect persistent state, use Prompt Intake Router and clarify or Plan Mode first.

---

## Operator Modes

Claudian can operate in three safe modes:

| Mode | Use When | Allowed Output |
| --- | --- | --- |
| Observe | The user wants analysis, search, explanation, or audit | Answer, source list, risk note, no writes |
| Capture | The user wants low-authority preservation | Draft, inbox note, record append, execution log |
| Governed Change | The user wants authority-changing edits | Proposal, review queue item, controlled update after approval |

Default to Observe when intent is unclear.

Default to Capture when information is useful but uncertain.

Default to Governed Change when current truth, rules, customer state, product facts, brand facts, permission, retrieval, security, or architecture may change.

---

## Non-Deployment Boundary

This document is a repository specification and template source.

It does not require creating a live Agent-Ops area on a personal computer.

When deploying inside an actual enterprise Vault, place copied protocol files into the ARMOR top-level structure. Do not add new top-level folders.

Forbidden deployment pattern:

```text
Vault/
└── 90-Agent-Ops/        # Do not create a new top-level layer.
```

ARMOR-native deployment pattern:

```text
Vault/
├── 00-Core/Agent-Protocols/
├── 05-Projects/Agent-Ops/
├── 92-Logs/Agent-Ops/
├── 93-Proposals/Agent-Ops/
└── 94-Review-Queues/Agent-Ops/
```

The top-level ARMOR structure remains frozen.

---

## Role Model

```text
Human Owner / Reviewer
        |
        | approves authority-changing proposals
        v
ARMOR Enterprise Vault
        |
        | stores governed memory, protocols, records, proposals
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
        | writes or proposes a task file
        v
05-Projects/Agent-Ops/Requests/pending/
        |
        | Claudian reads and executes according to ARMOR
        v
Vault change, proposal, record, draft, or execution log
```

Hermes is not required to run inside Claudian. Hermes may act as an external planner, reviewer, or task generator.

---

## What Claudian Can Add

Claudian can help ARMOR with execution capabilities:

```text
Read: load Vault files, @mention relevant notes, inspect project context.
Search: locate SSOT candidates, related rules, records, proposals, and conflicts.
Write: create drafts, records, proposals, logs, project notes, and allowed Class B/C files.
Edit: modify allowed files, prepare proposal diffs, apply approved low-risk changes.
Plan: use Plan Mode before high-risk or multi-step operations.
Coordinate: use file-based handoff requests and execution logs.
Extend: use slash commands, skills, MCP servers, and supported coding agents.
```

Claudian does not automatically enforce ARMOR governance. The executor must be instructed to follow the protocol and permission matrix before acting.

---

## What Claudian Must Not Bypass

Claudian's technical ability to edit files does not grant permission to edit them.

It must not:

- directly modify Class A files
- silently update current Facts
- treat Records as current Facts
- treat Drafts, Logs, Inbox, Raw Research, Proposals, or Archive as authoritative truth
- use runtime memory as durable business memory
- fix source errors by writing memory patches
- create new top-level Vault layers
- apply authority-changing proposals without human approval

If a task requires any of the above, Claudian must create a proposal or ask for human approval.

---

## ARMOR-Native Handoff Locations

Use existing ARMOR layers:

| Purpose | Vault Location | Authority |
| --- | --- | --- |
| Executor protocol files | `00-Core/Agent-Protocols/` | Class A, proposal-controlled |
| Pending task requests | `05-Projects/Agent-Ops/Requests/pending/` | Class B project workspace |
| Accepted task requests | `05-Projects/Agent-Ops/Requests/accepted/` | Class B project workspace |
| Completed task requests | `05-Projects/Agent-Ops/Requests/completed/` | Class B project workspace |
| Rejected task requests | `05-Projects/Agent-Ops/Requests/rejected/` | Class B project workspace |
| Execution logs | `92-Logs/Agent-Ops/` | Class C diagnostic logs |
| Authority-changing proposals | `93-Proposals/Agent-Ops/` | Class C proposal queue |
| Review queue summaries | `94-Review-Queues/Agent-Ops/` | Class C review queue |

These paths are recommended deployment locations inside a real enterprise Vault. They should not be created in a personal machine unless that machine is intentionally hosting the enterprise Vault.

---

## Execution Flow

```text
1. User or planner creates a task.
2. Prompt Intake Router classifies intent, risk, and persistence level.
3. If the task changes memory, Memory Write Router classifies destination.
4. If the task fixes an error, Root-Cause Fix Protocol identifies the source layer.
5. Claudian loads the task request and relevant ARMOR protocol files.
6. Claudian uses Plan Mode for multi-step, ambiguous, or high-risk work.
7. Claudian executes only allowed writes.
8. Class A or authority-changing edits become proposals.
9. Claudian writes an execution log.
10. Human reviewer approves, rejects, revises, or expires proposals.
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
@00-Core/Agent-Protocols/CLAUDIAN-ARMOR-OPERATING-PROTOCOL.md
@00-Core/Agent-Protocols/VAULT-WRITE-PERMISSION-MATRIX.md
@05-Projects/Agent-Ops/Requests/pending/{request-file}.md

Please execute this request according to ARMOR Enterprise.
Use Plan Mode first.
Do not modify Class A files directly.
Create proposals when required.
Write an execution log after completion.
```

---

## Success Criteria

A Claudian-assisted ARMOR deployment is working correctly when:

- Class A files are not directly modified by default
- Facts updates are preceded by SSOT search
- Records remain evidence, not current truth
- Drafts, Inbox, Logs, Raw Research, Proposals, and Archive stay out of default truth retrieval
- authority-changing requests create proposals
- execution logs describe what changed without becoming authority
- runtime memory can be cleared without losing business truth

Failure signals:

- "remember this" writes full content into runtime memory
- "fix this" creates a memory patch instead of repairing the source
- research or records are cited as current facts without labels
- Claudian creates new top-level Vault folders
- a proposal is treated as approved because it exists

---

## Template: Claudian ARMOR Operating Protocol

Recommended deployment path:

```text
00-Core/Agent-Protocols/CLAUDIAN-ARMOR-OPERATING-PROTOCOL.md
```

Template:

```markdown
# Claudian ARMOR Operating Protocol

## Role

You are the execution layer for an ARMOR Enterprise Vault.

You may read, search, summarize, classify, draft, append records, create project notes, create proposals, and write execution logs.

You must follow ARMOR's permission model before editing any Vault file.

## Non-Negotiable Rules

- Vault is the only durable business memory.
- Runtime memory is cache only.
- Capability does not equal permission.
- Capture does not equal authority.
- Write does not equal truth.
- SSOT must be checked before formal fact writes.
- Class A changes require proposal and human approval.
- Records are evidence, not current facts.
- Research is reference, not fact.
- Drafts, Inbox, Logs, Proposals, Raw Research, and Archive are excluded from default truth retrieval.
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
- P1: draft or low-authority note
- P2: normal project file
- P3: authoritative facts, rules, or long-term memory
- P4: Core, permission policy, retrieval policy, architecture, or SSOT map

If intent is ambiguous and persistence may be P2-P4, ask a concise clarification question or use Plan Mode before editing.

## Write Discipline

Before writing:

1. Identify knowledge type.
2. Identify source type.
3. Assign confidence label.
4. Determine memory class.
5. Search SSOT when target is authoritative.
6. Write lower when uncertain.
7. Create proposal when authority changes.
8. Add provenance metadata.
9. Write an execution log for significant work.

## Allowed Fast Writes

- `90-Drafts/`
- `91-Inbox/`
- `92-Logs/`
- `04-Research/00-Inbox/`
- `05-Projects/`
- `06-Records/` as append-only evidence
- `93-Proposals/`
- `94-Review-Queues/`

## Protected Writes

Do not directly modify:

- `00-Core/`
- `01-Facts/`
- `02-Rules/`
- `04-Research/01-Reviewed/`
- current-state customer, product, brand, security, retrieval, permission, or architecture files

Create a proposal instead.

## Completion Report

At the end of execution, report:

- Files read
- Files created
- Files modified
- Proposals created
- Records appended
- Logs written
- Items requiring human review
```

---

## Template: Vault Write Permission Matrix

Recommended deployment path:

```text
00-Core/Agent-Protocols/VAULT-WRITE-PERMISSION-MATRIX.md
```

Template:

```markdown
# Vault Write Permission Matrix

| Path | Class | Default Permission | Required Route |
| --- | --- | --- | --- |
| `00-Core/` | A | Read only | Proposal to `93-Proposals/Core/` |
| `01-Facts/` | A | Read only by default | SSOT search + proposal or controlled approved write |
| `02-Rules/` | A | Read only | Proposal to `93-Proposals/Rules/` |
| `03-Insights/` | B | Create/append allowed | Review for approved learnings or authority-changing edits |
| `04-Research/00-Inbox/` | C | Write allowed | Add source, confidence, freshness metadata when possible |
| `04-Research/01-Reviewed/` | B | Proposal or reviewed write | Source and review metadata required |
| `05-Projects/` | B | Create/append allowed | Proposal for current-state or authority-changing edits |
| `06-Records/` | R | Append only | Never rewrite history; corrections are new notes |
| `70-Schemas/` | A | Read only by default | Proposal for schema changes |
| `80-Indexes/` | B | Update allowed when derived | Must not create authority |
| `81-Dashboards/` | B | Update allowed when derived | Must not create authority |
| `90-Drafts/` | C | Write allowed | Excluded from default retrieval |
| `91-Inbox/` | C | Write allowed | Triage later |
| `92-Logs/` | C | Write allowed | Diagnostic only |
| `93-Proposals/` | C | Write allowed | Pending until reviewed |
| `94-Review-Queues/` | C | Write allowed | Queue only |
| `99-Archive/` | Archive | Historical only | Do not use as current truth |

## Approval Rule

If a requested edit changes current truth, future behavior, customer current state, product facts, brand facts, approved rules, security posture, permission policy, retrieval behavior, or conflict resolution, create a proposal instead of directly editing the target file.
```

---

## Template: Hermes Handoff Protocol

Recommended deployment path:

```text
00-Core/Agent-Protocols/HERMES-HANDOFF-PROTOCOL.md
```

Template:

```markdown
# Hermes Handoff Protocol

## Purpose

This protocol defines how Hermes-style planners hand tasks to Claudian-style Vault executors through ARMOR-governed files.

## Handoff Principle

Hermes does not need to run inside Claudian.

Hermes writes or proposes task requests into the Vault. Claudian reads those requests and executes them according to ARMOR.

## Request Path

```text
05-Projects/Agent-Ops/Requests/pending/
```

## Request Lifecycle

```text
pending -> accepted -> completed
pending -> rejected
pending -> proposal-required
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
- Allowed actions
- Forbidden actions
- Expected output
- Review requirement

## Executor Responsibilities

Claudian must:

1. Read this handoff protocol.
2. Read the task request.
3. Read the Claudian ARMOR Operating Protocol.
4. Read the Vault Write Permission Matrix.
5. Use Plan Mode for ambiguous, multi-step, or high-risk work.
6. Execute allowed writes only.
7. Create proposals for protected changes.
8. Write an execution log.

## Planner Responsibilities

Hermes should:

1. Classify intent before creating a request.
2. Avoid embedding unbounded context into request files.
3. Link relevant SSOT, Rules, Records, Projects, or Proposals.
4. Mark uncertainty and risk explicitly.
5. Avoid asking Claudian to bypass ARMOR permission rules.
```

---

## Template: Agent Request

Recommended deployment path:

```text
05-Projects/Agent-Ops/Requests/pending/REQ-YYYY-MM-DD-001.md
```

Template:

```markdown
---
type: agent_request
memory_layer: projects
status: pending
authority: provisional
created: YYYY-MM-DD
updated: YYYY-MM-DD
created_by: Hermes
target_executor: Claudian
request_id: REQ-YYYY-MM-DD-001
risk: low | medium | high
persistence_level: P0 | P1 | P2 | P3 | P4
write_policy: governed
retrieval_scope: excluded
---

# Agent Request: {Title}

## User Intent

What the user wants.

## Task Type

direct_task | memory_write | root_cause_fix | research | project_work | audit | cleanup | proposal_apply

## Relevant Files

- `00-Core/...`
- `01-Facts/...`
- `02-Rules/...`

## Required Protocols

- `00-Core/Agent-Protocols/CLAUDIAN-ARMOR-OPERATING-PROTOCOL.md`
- `00-Core/Agent-Protocols/VAULT-WRITE-PERMISSION-MATRIX.md`

## Allowed Actions

- Read relevant files
- Search for SSOT
- Create drafts
- Append records
- Create proposals
- Update allowed project files
- Write execution log

## Forbidden Actions

- Do not directly modify Class A files.
- Do not treat Records as current Facts.
- Do not use Drafts, Inbox, Logs, Raw Research, Proposals, or Archive as current truth.
- Do not create new top-level Vault folders.
- Do not apply authority-changing edits without approval.

## Expected Output

- Draft / Record / Proposal / Project update / Execution log

## Review Requirement

No review required | Human review required | Proposal required

## Completion Notes

Filled by executor.
```

---

## Template: Execution Log

Recommended deployment path:

```text
92-Logs/Agent-Ops/YYYY-MM-DD-{request-id}.md
```

Template:

```markdown
---
type: log
memory_layer: logs
status: active
authority: none
created: YYYY-MM-DD
updated: YYYY-MM-DD
source: agent_execution
write_policy: open
retrieval_scope: debug_only
request_id:
executor: Claudian
---

# Agent Execution Log: {Request ID}

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

## Proposals Created

## Records Appended

## Checks Performed

- SSOT search:
- Permission check:
- Confidence classification:
- Source/provenance check:
- Schema check:

## Human Review Needed

## Result

## Notes

Logs are diagnostic only and must not be treated as authoritative memory.
```

---

## Minimal Deployment Checklist

For an actual enterprise Vault:

1. Copy the protocol templates into `00-Core/Agent-Protocols/`.
2. Create `05-Projects/Agent-Ops/Requests/` only if the Vault will use file-based handoff.
3. Create `92-Logs/Agent-Ops/` for execution logs.
4. Create `93-Proposals/Agent-Ops/` only when agent-operation proposals are needed.
5. Configure Claudian users to load the operating protocol and permission matrix before executing requests.
6. Use Plan Mode for high-risk, ambiguous, or multi-step edits.
7. Never allow Claudian to directly modify Class A files.
8. Audit retrieval settings to ensure low-authority layers do not enter default truth retrieval.

---

## Final Principle

Claudian can make ARMOR operational, but it must remain an executor under ARMOR governance.

The correct relationship is:

```text
Claudian gives the agent hands.
ARMOR decides what the hands may touch.
The Vault records what happened.
Human review approves changes to truth.
```

# PAMA Personal Execution Workflow

> Lightweight execution templates for complex personal tasks, goals, and reviews.
>
> This workflow borrows the practical rhythm of file-based planning, but keeps it inside PAMA's low-authority working layers. It is not a second memory architecture, not a hook system, and not a path around PAMA routers or user sovereignty.

## Purpose

Use this workflow when a personal task is large enough that normal conversation context is likely to lose important state.

Typical triggers:

- the task needs five or more tool calls
- the task spans multiple sessions or agents
- the task is tied to a goal, decision, review, or personal project
- the task includes research, execution, reflection, and follow-up
- the user asks the agent to keep progress visible

Skip this workflow for simple answers, one-step lookups, or casual discussion.

## Recommended Location

If the task belongs to an active goal, create one execution folder under that goal:

```text
04-Goals/<goal-name>/Execution/YYYY-MM-DD-<task-slug>/
  task_plan.md
  findings.md
  progress.md
  closeout.md
```

If the task is not clearly tied to a goal yet, use working memory:

```text
08-Working-Memory/Execution/YYYY-MM-DD-<task-slug>/
  task_plan.md
  findings.md
  progress.md
  closeout.md
```

Do not add a new top-level Vault layer for execution files.

## Authority Model

Execution files are working materials.

| File | PAMA role | Default authority | Default retrieval |
| --- | --- | --- | --- |
| `task_plan.md` | Personal task or goal execution plan | Low | Current task only |
| `findings.md` | Candidate observations, hypotheses, notes | Low | Excluded from personal truth |
| `progress.md` | Execution log | Low | Current task only |
| `closeout.md` | Reflection and routing checklist | Medium candidate | Review-scoped only |

Rules:

- `findings.md` is not `01-Reality/`.
- `progress.md` is not a decision record.
- `task_plan.md` is not a goal source of truth.
- `closeout.md` may identify candidate memory, but it does not promote memory by itself.
- Nothing in this workflow may bypass `PAMA_Memory_Write_Router.md`, `PAMA_Root_Cause_Fix_Protocol.md`, review gates, or user approval.

## Promotion Boundary

When an execution file contains something worth preserving, route it through PAMA.

```text
task execution note
  -> findings.md or progress.md
  -> closeout.md candidate list
  -> PAMA Memory Write Router or PAMA Root-Cause Fix Protocol
  -> 08-Working-Memory / 06-Meta / 07-Reviews / 01-Reality / 03-Decisions / 04-Goals
  -> 05-Truth only after review or explicit user approval
```

Direct promotion from `findings.md`, `progress.md`, `task_plan.md`, or `closeout.md` into `05-Truth/` is forbidden unless the user explicitly approves the exact truth-changing edit through the PAMA review or memory routing process.

## Operating Pattern

1. Create the execution folder and copy the four templates.
2. Fill `task_plan.md` with goal, scope, phases, and acceptance checks.
3. Record observations, hypotheses, and source-backed notes in `findings.md`.
4. Record actions, verification, failures, and files touched in `progress.md`.
5. At task end, write `closeout.md`.
6. Route candidate memory through the correct PAMA router or review gate.

## Complexity Control

This workflow intentionally avoids:

- runtime hooks
- automatic plan injection
- automatic stop gates
- hash attestation
- runtime-specific session recovery
- cross-agent plugin parity
- additional top-level Vault folders

Those features may be useful in execution tools, but they increase maintenance cost. PAMA should keep this workflow as a template-level convention unless the user explicitly asks for automation later.

## Template Files

Repository templates live in:

```text
personal/templates/personal_execution/
```

Suggested installed Vault location:

```text
08-Working-Memory/Templates/Personal-Execution/
```

Agents may copy these templates into a goal or working-memory execution folder when starting a complex personal task.

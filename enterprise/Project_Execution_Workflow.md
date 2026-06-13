# ARMOR Project Execution Workflow

> Lightweight project execution templates for complex agent tasks.
>
> This workflow borrows the practical three-file rhythm of file-based planning, but keeps it inside ARMOR's low-authority execution layer. It is not a second memory architecture, not a hook system, and not an authority path around ARMOR routers.

## Purpose

Use this workflow when an agent task is large enough that normal chat context is likely to lose important state.

Typical triggers:

- the task needs five or more tool calls
- the task spans multiple sessions or agents
- the task includes research, implementation, validation, and delivery
- the task has meaningful risk, rollback, or open questions
- the user asks the agent to keep progress visible

Skip this workflow for simple answers, quick edits, or one-step lookups.

## Recommended Location

Create one execution folder under the relevant active project:

```text
05-Projects/<project-name>/Execution/YYYY-MM-DD-<task-slug>/
  task_plan.md
  findings.md
  progress.md
  closeout.md
```

If no project exists yet, create the execution folder under the most appropriate active project workspace or capture the task in `90-Drafts/` until the project location is clear.

Do not add a new top-level Vault layer for execution files.

## Authority Model

Execution files are working materials.

| File | ARMOR role | Default authority | Default retrieval |
| --- | --- | --- | --- |
| `task_plan.md` | Project execution plan | Low or conditional | Project-scoped only |
| `findings.md` | Candidate discoveries and notes | Low | Excluded from current truth |
| `progress.md` | Execution log | Low | Excluded from current truth |
| `closeout.md` | Completion summary and promotion checklist | Medium candidate | Project-scoped only |

Rules:

- `findings.md` is not a fact file.
- `progress.md` is not a rule file.
- `task_plan.md` is not a source of truth map.
- `closeout.md` may identify candidate memory, but it does not promote memory by itself.
- Nothing in this workflow may bypass `Memory_Write_Router.md`, `Root_Cause_Fix_Protocol.md`, or the ARMOR permission model.

## Promotion Boundary

When an execution file contains something worth preserving, route it through ARMOR.

```text
task execution note
  -> findings.md or progress.md
  -> closeout.md candidate list
  -> Memory Write Router or Root-Cause Fix Protocol
  -> 91-Inbox / 90-Drafts / 93-Proposals / 04-Research / 03-Insights
  -> approved authority layer only when allowed
```

Direct promotion from `findings.md` to `01-Facts/` or `02-Rules/` is forbidden unless the user explicitly approves the exact authority-changing edit and the agent has checked the existing SSOT.

## Operating Pattern

1. Create the execution folder and copy the four templates.
2. Fill `task_plan.md` with goal, scope, phases, and acceptance checks.
3. Record discoveries in `findings.md` with source and confidence.
4. Record actions, test results, failures, and files touched in `progress.md`.
5. At task end, write `closeout.md`.
6. Route any candidate long-term memory through the correct ARMOR router.

## Complexity Control

This workflow intentionally avoids:

- runtime hooks
- automatic plan injection
- automatic stop gates
- hash attestation
- runtime-specific session recovery
- cross-agent plugin parity
- additional top-level Vault folders

Those features are useful in execution tools, but they increase architecture maintenance cost. ARMOR should keep this workflow as a template-level convention unless a specific deployment needs automation later.

## Template Files

Repository templates live in:

```text
enterprise/templates/project_execution/
```

Suggested installed Vault location:

```text
70-Schemas/Project-Execution/
```

Agents may copy these templates into a project execution folder when starting a complex task.

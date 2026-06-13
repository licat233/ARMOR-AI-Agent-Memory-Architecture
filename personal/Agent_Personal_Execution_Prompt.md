# Agent Personal Execution Prompt

> Copy-ready prompt snippets for agents that should use the PAMA lightweight personal execution workflow.
>
> Applies to: AI Agent Memory Architecture v1.2.4, PAMA Personal V5.3 Stable.

## Purpose

Use this document when configuring an agent such as Codex, Hermes, Claude Code, Opencode, Cline, OpenHands, or a custom runtime to operate a PAMA Personal Vault.

The goal is to teach the agent when and how to use PAMA execution files without turning them into personal truth, identity, or durable preference.

## Recommended Placement

Use the shortest durable rule surface available for the agent.

| Runtime | Recommended placement |
| --- | --- |
| Codex | Project `AGENTS.md`, global Codex instructions, or a PAMA skill/reference file |
| Hermes | PAMA profile instructions, SOUL rule, or PAMA skill |
| Claude Code | Project `CLAUDE.md`, user `CLAUDE.md`, or project skill instructions |
| Opencode / Cline / OpenHands | Project agent instructions or equivalent runtime rule file |
| Custom agent | System prompt or startup instruction file |

Do not paste the full personal execution templates into the agent's permanent system prompt. Keep the rule short and point the agent to the Vault templates.

## Minimal System Prompt Snippet

Copy this into the agent's persistent instructions:

```md
## PAMA Personal Execution Workflow

When working inside a PAMA Personal Vault, use the lightweight personal execution workflow for complex personal tasks, goals, or reviews.

Use it only when the task is complex, spans multiple steps or sessions, involves research plus execution, or needs visible progress tracking.

If the task belongs to an active goal, create execution files under:

04-Goals/<goal-name>/Execution/YYYY-MM-DD-<task-slug>/

If the task is not clearly tied to a goal, use:

08-Working-Memory/Execution/YYYY-MM-DD-<task-slug>/

Use these files:
- task_plan.md for goal, scope, phases, risks, and acceptance checks
- findings.md for candidate observations, hypotheses, and source-backed notes
- progress.md for execution log, verification, files touched, and errors
- closeout.md for final reflection and candidate memory routing

Execution files are low-authority working materials. They are not Reality, Decisions, Goals source of truth, Truth, or approved memory.

Do not promote content from task_plan.md, findings.md, progress.md, or closeout.md directly into 05-Truth/.

Candidate long-term memory must go through PAMA-Memory-Write-Router.md, PAMA-Root-Cause-Fix-Protocol.md, or a review gate.

Do not add hooks, automatic plan injection, stop gates, attestation, runtime-specific recovery automation, or new top-level Vault folders unless explicitly requested.

If the templates exist, read them from:

08-Working-Memory/Templates/Personal-Execution/
```

## Install-Time Agent Prompt

Use this when asking an agent to configure itself for a PAMA Vault:

```text
Please configure your persistent project instructions to use the PAMA lightweight personal execution workflow.

Read this repository document first:
personal/Agent_Personal_Execution_Prompt.md

Then add the Minimal System Prompt Snippet to your appropriate persistent instruction location.

For Codex, use AGENTS.md or the configured PAMA reference/skill.
For Hermes, use the PAMA profile instruction, SOUL rule, or PAMA skill.
For Claude Code, use CLAUDE.md or project skill instructions.

Do not copy the full templates into your system prompt.
Do not add runtime hooks or automation.
Do not create new top-level Vault folders.

After configuration, verify that your rule says:
1. Use the workflow only for complex personal work.
2. Store goal-tied execution files under 04-Goals/<goal-name>/Execution/YYYY-MM-DD-<task-slug>/.
3. Store unclear execution files under 08-Working-Memory/Execution/YYYY-MM-DD-<task-slug>/.
4. Treat execution files as low-authority working materials.
5. Route candidate long-term memory through PAMA routers or reviews.
```

## Codex AGENTS.md Snippet

Use this in a Codex project `AGENTS.md`:

```md
## PAMA Personal Execution Workflow

For complex PAMA personal work, use the lightweight personal execution templates from AI Agent Memory Architecture v1.2.4.

For goal-tied tasks, create execution files under `04-Goals/<goal-name>/Execution/YYYY-MM-DD-<task-slug>/`.

For unclear or temporary tasks, create execution files under `08-Working-Memory/Execution/YYYY-MM-DD-<task-slug>/`.

Use `task_plan.md`, `findings.md`, `progress.md`, and `closeout.md` only as low-authority working materials.

Do not treat these files as Reality, Decisions, Goals source of truth, Truth, or approved memory.

Route candidate long-term memory through `00-Core/PAMA-Memory-Write-Router.md`, `00-Core/PAMA-Root-Cause-Fix-Protocol.md`, or `07-Reviews/`.

Do not add hooks, automatic plan injection, stop gates, attestation, or new top-level Vault folders unless explicitly requested.
```

## Hermes Prompt Snippet

Use this in the Hermes PAMA profile, SOUL rule, or PAMA skill:

```md
## PAMA Personal Execution Workflow

For complex PAMA personal tasks, create a low-authority execution folder.

Goal-tied tasks:

04-Goals/<goal-name>/Execution/YYYY-MM-DD-<task-slug>/

Unclear or temporary tasks:

08-Working-Memory/Execution/YYYY-MM-DD-<task-slug>/

Use `task_plan.md`, `findings.md`, `progress.md`, and `closeout.md` from `08-Working-Memory/Templates/Personal-Execution/` when available.

These files are execution scaffolding only. They do not override PAMA governance, user sovereignty, Memory Write Router, Root-Cause Fix Protocol, review gates, or runtime memory policy.

Candidate reality, decisions, goals, truth, hypotheses, or preferences must be routed before becoming durable memory.
```

## Claude Code CLAUDE.md Snippet

Use this in project or user `CLAUDE.md`:

```md
## PAMA Personal Execution Workflow

When a task inside a PAMA Vault is multi-step or long-running, use the optional personal execution templates.

Goal-tied location:

04-Goals/<goal-name>/Execution/YYYY-MM-DD-<task-slug>/

Working-memory fallback:

08-Working-Memory/Execution/YYYY-MM-DD-<task-slug>/

Files:
- task_plan.md
- findings.md
- progress.md
- closeout.md

Treat these as low-authority execution files. They are not approved personal memory and do not replace PAMA routers or reviews.

Before writing anything into Reality, Decisions, Goals, Truth, or reviewed lessons, follow the relevant PAMA router and review policy.
```

## Verification Checklist

After an agent configures itself, check that:

- The rule is short enough to keep in persistent instructions.
- The rule points to `08-Working-Memory/Templates/Personal-Execution/` instead of embedding all templates.
- The rule says execution files are low-authority.
- The rule forbids direct promotion to `05-Truth/`.
- The rule preserves PAMA user sovereignty and review gates.
- The rule does not introduce hooks, automatic injection, stop gates, attestation, or new top-level Vault folders.

## Maintenance Rule

If this workflow changes, update this document and the templates first. Agent prompts should remain short pointers to the maintained Vault documentation.

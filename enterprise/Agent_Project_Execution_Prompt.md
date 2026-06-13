# Agent Project Execution Prompt

> Copy-ready prompt snippets for agents that should use the ARMOR lightweight project execution workflow.
>
> Applies to: AI Agent Memory Architecture v1.2.4, ARMOR Enterprise V7.2 Stable.

## Purpose

Use this document when configuring an agent such as Codex, Hermes, Claude Code, Opencode, Cline, OpenHands, or a custom runtime.

The goal is to teach the agent when and how to use ARMOR project execution files without turning them into a second memory system.

## Recommended Placement

Use the shortest durable rule surface available for the agent.

| Runtime | Recommended placement |
| --- | --- |
| Codex | Project `AGENTS.md`, global Codex instructions, or an ARMOR skill/reference file |
| Hermes | ARMOR profile instructions, SOUL rule, or ARMOR skill |
| Claude Code | Project `CLAUDE.md`, user `CLAUDE.md`, or project skill instructions |
| Opencode / Cline / OpenHands | Project agent instructions or equivalent runtime rule file |
| Custom agent | System prompt or startup instruction file |

Do not paste the full project execution templates into the agent's permanent system prompt. Keep the rule short and point the agent to the Vault templates.

## Minimal System Prompt Snippet

Copy this into the agent's persistent instructions:

```md
## ARMOR Project Execution Workflow

When working inside an ARMOR Enterprise Vault, use the lightweight project execution workflow for complex project tasks.

Use it only when the task is complex, spans multiple steps or sessions, involves research plus execution, or needs visible progress tracking.

Create execution files under:

05-Projects/<project-name>/Execution/YYYY-MM-DD-<task-slug>/

Use these files:
- task_plan.md for goal, scope, phases, risks, and acceptance checks
- findings.md for candidate discoveries and source-backed notes
- progress.md for execution log, verification, files touched, and errors
- closeout.md for final summary and candidate memory routing

Execution files are low-authority working materials. They are not Core policy, Facts, Rules, or approved memory.

Do not promote content from task_plan.md, findings.md, progress.md, or closeout.md directly into 01-Facts/ or 02-Rules/.

Candidate long-term memory must go through Memory-Write-Router.md, Root-Cause-Fix-Protocol.md, or the proposal workflow.

Do not add hooks, automatic plan injection, stop gates, attestation, runtime-specific recovery automation, or new top-level Vault folders unless explicitly requested.

If the templates exist, read them from:

70-Schemas/Project-Execution/
```

## Install-Time Agent Prompt

Use this when asking an agent to configure itself for an ARMOR Vault:

```text
Please configure your persistent project instructions to use the ARMOR lightweight project execution workflow.

Read this repository document first:
enterprise/Agent_Project_Execution_Prompt.md

Then add the Minimal System Prompt Snippet to your appropriate persistent instruction location.

For Codex, use AGENTS.md or the configured Codex ARMOR reference/skill.
For Hermes, use the ARMOR profile instruction, SOUL rule, or ARMOR skill.
For Claude Code, use CLAUDE.md or project skill instructions.

Do not copy the full templates into your system prompt.
Do not add runtime hooks or automation.
Do not create new top-level Vault folders.

After configuration, verify that your rule says:
1. Use the workflow only for complex project work.
2. Store execution files under 05-Projects/<project-name>/Execution/YYYY-MM-DD-<task-slug>/.
3. Treat execution files as low-authority working materials.
4. Route candidate long-term memory through ARMOR routers or proposals.
```

## Codex AGENTS.md Snippet

Use this in a Codex project `AGENTS.md`:

```md
## ARMOR Project Execution Workflow

For complex ARMOR project work, use the lightweight project execution templates from AI Agent Memory Architecture v1.2.4.

Create execution files under `05-Projects/<project-name>/Execution/YYYY-MM-DD-<task-slug>/`.

Use `task_plan.md`, `findings.md`, `progress.md`, and `closeout.md` only as low-authority working materials.

Do not treat these files as current facts, rules, or Core policy.

Route candidate long-term memory through `00-Core/Memory-Write-Router.md`, `00-Core/Root-Cause-Fix-Protocol.md`, or `93-Proposals/`.

Do not add hooks, automatic plan injection, stop gates, attestation, or new top-level Vault folders unless explicitly requested.
```

## Hermes Prompt Snippet

Use this in the Hermes ARMOR profile, SOUL rule, or ARMOR skill:

```md
## ARMOR Project Execution Workflow

For complex ARMOR project tasks, create a low-authority execution folder:

05-Projects/<project-name>/Execution/YYYY-MM-DD-<task-slug>/

Use `task_plan.md`, `findings.md`, `progress.md`, and `closeout.md` from `70-Schemas/Project-Execution/` when available.

These files are execution scaffolding only. They do not override the ARMOR Vault governance model, Memory Write Router, Root-Cause Fix Protocol, permission model, or proposal workflow.

Candidate business facts, rules, product knowledge, customer state, and architecture changes must be routed before becoming durable memory.
```

## Claude Code CLAUDE.md Snippet

Use this in project or user `CLAUDE.md`:

```md
## ARMOR Project Execution Workflow

When a task inside an ARMOR Vault is multi-step or long-running, use the optional project execution templates.

Location:

05-Projects/<project-name>/Execution/YYYY-MM-DD-<task-slug>/

Files:
- task_plan.md
- findings.md
- progress.md
- closeout.md

Treat these as low-authority execution files. They are not approved memory and do not replace ARMOR routers.

Before writing anything into Facts, Rules, Core, reviewed research, or validated insights, follow the relevant ARMOR router and permission policy.
```

## Verification Checklist

After an agent configures itself, check that:

- The rule is short enough to keep in persistent instructions.
- The rule points to `70-Schemas/Project-Execution/` instead of embedding all templates.
- The rule says execution files are low-authority.
- The rule forbids direct promotion to `01-Facts/` and `02-Rules/`.
- The rule does not introduce hooks, automatic injection, stop gates, attestation, or new top-level Vault folders.
- The rule preserves ARMOR's existing routers and proposal workflow.

## Maintenance Rule

If this workflow changes, update this document and the templates first. Agent prompts should remain short pointers to the maintained Vault documentation.

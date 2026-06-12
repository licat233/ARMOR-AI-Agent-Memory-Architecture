# Agent Installation Guide

> Give this file to an AI agent so it can install AI Agent Memory Architecture into an Obsidian Vault or trusted Markdown directory.
>
> Default install: `enterprise` / ARMOR Enterprise AI Workspace.
>
> This is an architecture installation, not a software package installation. Do not install Obsidian UI plugins. Do not treat runtime memory, embeddings, SQLite, or indexes as the durable memory source.

---

## 1. Default Behavior

Install ARMOR Enterprise AI Workspace by default.

The user only needs to provide a target Vault or Markdown directory path.

Do not ask the user to choose between `enterprise`, `personal`, or `both` unless they explicitly request a non-default installation.

If the target path is provided, proceed with enterprise installation.

If the target path is missing, ask one question:

```text
What target Vault or Markdown directory should I install ARMOR into?
```

---

## 2. Install Goal

Create a governed enterprise memory Vault for AI agents.

The installed Vault must preserve these principles:

- The Vault is the durable source of truth.
- Runtime memory is temporary and low-authority.
- Uncertain information is stored lower.
- Authoritative memory requires evidence, review, and correct routing.
- High-authority changes require proposal or explicit human approval.
- Drafts, inboxes, logs, raw records, proposals, and archives are excluded from default truth retrieval.

---

## 3. Safe Install Rules

Before writing:

1. Resolve the target path.
2. If the path does not exist, create it.
3. If the path exists, inspect it briefly.
4. Create missing directories only.
5. Copy missing core documents only.
6. Never overwrite existing files silently.
7. If a target file already exists, preserve it and write a timestamped candidate under `93-Proposals/` or `90-Drafts/`.

The user's request to install is enough permission to create missing directories and missing architecture files inside the target path.

Ask for confirmation only when an existing file would be overwritten, renamed, deleted, or structurally changed.

---

## 4. Source Repository Assumptions

The installer should be run from a local checkout of this repository or from a location where these files are available:

```text
README.md
enterprise/
personal/
```

If the repository is not available locally, ask the user to provide the path or clone:

```text
https://github.com/licat233/AI-Agent-Memory-Architecture.git
```

Do not download or install additional tools unless the user explicitly approves.

---

## 5. Default Enterprise Installation: ARMOR

### 5.1 Create Top-Level Directories

Create these directories inside the target Vault if missing:

```text
00-Core/
01-Facts/
02-Rules/
03-Insights/
04-Research/
04-Research/00-Inbox/
04-Research/01-Reviewed/
05-Projects/
06-Records/
70-Schemas/
80-Indexes/
81-Dashboards/
90-Drafts/
91-Inbox/
92-Logs/
93-Proposals/
94-Review-Queues/
99-Archive/
```

Do not rename, merge, or invent top-level layers without explicit user approval.

### 5.2 Copy Core ARMOR Documents

Copy these repository files into the target Vault if missing:

| Source | Destination |
| --- | --- |
| `enterprise/V7_2_Stable.md` | `00-Core/ARMOR-V7.2-Stable.md` |
| `enterprise/V7_1_5_Governance_Patch.md` | `00-Core/ARMOR-Governance-Patch-V7.1.5.md` |
| `enterprise/Prompt_Intake_Router.md` | `00-Core/Prompt-Intake-Router.md` |
| `enterprise/Memory_Write_Router.md` | `00-Core/Memory-Write-Router.md` |
| `enterprise/Root_Cause_Fix_Protocol.md` | `00-Core/Root-Cause-Fix-Protocol.md` |
| `enterprise/Runtime_Memory_Policy.md` | `00-Core/Runtime-Memory-Policy.md` |
| `enterprise/agent_runtime_adaptation_guide.md` | `00-Core/Agent-Runtime-Adaptation-Guide.md` |
| `enterprise/multi_agent_shared_vault_governance.md` | `00-Core/Multi-Agent-Shared-Vault-Governance.md` |

If a destination file already exists, do not overwrite it. Preserve the file and create a candidate copy under:

```text
93-Proposals/Install-Candidates/
```

### 5.3 Create Starter Core Files

If missing, create these small placeholder files:

```text
00-Core/Source-of-Truth-Map.md
00-Core/Permission-Policy.md
00-Core/Retrieval-Rules.md
00-Core/Lifecycle-Policy.md
00-Core/Installed-Memory-Architecture.md
```

Each placeholder should state that it must follow ARMOR V7.2 and the governance patch.

---

## 6. Runtime Integration

After installing files, explain this to the user and the operating agent:

```text
The Vault is long-term memory.
The agent runtime provides capability.
Runtime memory, SQLite, embeddings, and indexes are temporary infrastructure.
They are not authoritative memory.
```

Any trusted runtime can operate the Vault if it has file read/search/write/patch capability and follows ARMOR governance.

Examples:

- Hermes
- Claude Code
- Codex
- Opencode
- Cline
- OpenHands
- custom agents
- MCP-backed agents

The runtime should:

- point its long-term memory or workspace path to the installed Vault
- use `00-Core/Prompt-Intake-Router.md` before ambiguous, high-risk, fix, or remember requests
- use `00-Core/Memory-Write-Router.md` before storing permanent memory
- use `00-Core/Root-Cause-Fix-Protocol.md` when correcting errors
- use `00-Core/Runtime-Memory-Policy.md` to keep runtime memory temporary and low-authority
- use `00-Core/Multi-Agent-Shared-Vault-Governance.md` when multiple agents share the same Vault

For Codex, prefer a local reference plus a skill rather than writing durable facts into Codex runtime memory:

```text
~/.codex/memory/reference_armor_vault.md
~/.codex/skills/armor-enterprise-vault/SKILL.md
```

The reference should point to the installed Vault, and the skill should instruct Codex to read the ARMOR routers and policies before memory-related writes.

For multi-agent deployments, create starter namespaces when useful:

```text
91-Inbox/{agent-name}/
92-Logs/{agent-name}/
93-Proposals/{agent-name}/
93-Proposals/Conflicts/
```

---

## 7. Installation Log

Write an installation log after successful installation:

```text
92-Logs/YYYY-MM-DD-Memory-Architecture-Install.md
```

The log should include:

```yaml
architecture: ARMOR
project_version: v1.1.0
version: V7.2 Stable
installed_at: YYYY-MM-DD
source_repository: AI-Agent-Memory-Architecture
target_vault: /absolute/path
agent_runtime: unknown | Hermes | Claude Code | Codex | Opencode | Cline | OpenHands | other
files_created:
files_copied:
existing_files_preserved:
candidate_files_created:
open_questions:
```

If the runtime is unknown, write `unknown`. Do not block installation just to identify the runtime.

---

## 8. Validation Checklist

Before reporting completion, verify:

- The target Vault exists.
- Required ARMOR top-level directories exist.
- Core architecture documents were copied or preserved.
- Existing user files were not overwritten silently.
- `93-Proposals/` exists.
- `06-Records/` exists.
- `90-Drafts/`, `91-Inbox/`, and `92-Logs/` exist.
- `00-Core/Memory-Write-Router.md` exists.
- Runtime memory was not configured as the durable source of truth.
- No Obsidian UI plugin was installed.
- The installation log exists.
- The user knows which path to point their AI agent at.
- Multi-agent deployments have a namespace and conflict policy.

---

## 9. Advanced Options

Only use these if the user explicitly asks.

### Personal / PAMA

Install PAMA instead of ARMOR when the user explicitly asks for personal memory, personal reality tracking, personal decisions, goals, or attention review.

Use the personal files under `personal/` and create the PAMA directory structure described in `personal/README.md` and `personal/PAMA V5.2 Stable.md`.

For PAMA multi-agent deployments, also copy:

| Source | Destination |
| --- | --- |
| `personal/PAMA_Multi_Agent_Shared_Vault_Governance.md` | `00-Core/PAMA-Multi-Agent-Shared-Vault-Governance.md` |

Create starter namespaces when useful:

```text
08-Working-Memory/{agent-name}/
08-Working-Memory/Memory-Candidates/{agent-name}/
08-Working-Memory/Fix-Candidates/{agent-name}/
08-Working-Memory/Logs/{agent-name}/
07-Reviews/{agent-name}/
07-Reviews/Promotion-Candidates/
07-Reviews/Conflict-Reviews/
```

PAMA shared Vault deployments must preserve user sovereignty. Agents must not directly promote material into `05-Truth/`, rewrite goals, or change major decisions without explicit user approval or a review decision.

### Both

If the user asks for both enterprise and personal memory, recommend separate Vault roots:

```text
Memory-Vaults/
  ARMOR-Enterprise/
  PAMA-Personal/
```

Do not mix `01-Facts/` and `01-Reality/` in one top-level Vault unless the user explicitly approves a custom combined architecture.

### Custom Runtime

If the user names a specific runtime, adapt only the final runtime instructions. Do not change the Vault structure unless the architecture requires it.

---

## 10. Completion Response

After installation, report:

1. Installed architecture: ARMOR Enterprise AI Workspace.
2. Target Vault path.
3. Core documents copied.
4. Existing files preserved or candidate files created.
5. Installation log path.
6. The next instruction the user's AI agent should follow.

Keep the response concise. Do not claim that memory has been promoted into truth unless the appropriate review or proposal process happened.

---

## 11. Final Rule

Installing the architecture only creates the governed memory system.

It does not make every future note authoritative.

The agent must continue to follow the routers, permission model, retrieval policy, runtime memory policy, and proposal workflow every time it reads or writes memory.

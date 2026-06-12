# Agent Update Guide

This guide is for AI agents updating an existing Vault or Markdown workspace to a newer version of AI Agent Memory Architecture.

It is intentionally different from `AGENT_INSTALL.md`.

Installation answers:

```text
How do I create the architecture?
```

Update answers:

```text
How do I align an existing Vault with the latest architecture without leaving stale active files behind?
```

Current target:

```text
AI Agent Memory Architecture v1.2.2
ARMOR Enterprise V7.2 Stable
PAMA Personal V5.3 Stable
```

## Core Principle

Do not overwrite history to make search results look clean.

Instead:

- update active authority files
- add missing current files
- archive superseded active files
- mark superseded proposals
- leave logs, records, decisions, and archive files as historical evidence unless the user explicitly asks to rewrite them

Runtime memory, embeddings, indexes, local databases, and session summaries are not long-term memory. They may be rebuilt after the Vault is aligned.

## Update Prompt

Users can give this prompt to an AI agent:

```text
Please read and execute AGENT_UPDATE.md from this repository:
https://github.com/licat233/AI-Agent-Memory-Architecture

Help me update my existing AI Agent Memory Architecture Vault.
Target architecture: AI Agent Memory Architecture v1.2.2.
Default branch: ARMOR Enterprise V7.2 Stable unless I explicitly say PAMA Personal.
Target Vault path: <paste your Vault or Markdown directory path here>

Do not install any Obsidian UI plugin.
Do not use runtime memory as long-term memory.
Preserve user content and history.
Archive superseded active files instead of deleting them.
Update active Core, Indexes, runtime adaptation guides, routers, and governance files.
Mark obsolete pending proposals as superseded when they point to retired files.
Do not rewrite logs, records, decisions, or archive files unless they are being used as current truth.
Write an update log and run the validation checklist.
```

## Required First Reads

Before changing files, read:

```text
README.md
AGENT_INSTALL.md
AGENT_UPDATE.md
```

For ARMOR updates, also read:

```text
enterprise/README.md
enterprise/V7_2_Stable.md
enterprise/V7_1_5_Governance_Patch.md
enterprise/agent_runtime_adaptation_guide.md
enterprise/multi_agent_shared_vault_governance.md
enterprise/Prompt_Intake_Router.md
enterprise/Memory_Write_Router.md
enterprise/Root_Cause_Fix_Protocol.md
enterprise/Runtime_Memory_Policy.md
```

For PAMA updates, also read:

```text
personal/README.md
personal/PAMA V5.3 Stable.md
personal/PAMA_Multi_Agent_Shared_Vault_Governance.md
personal/PAMA_Prompt_Intake_Router.md
personal/PAMA_Memory_Write_Router.md
personal/PAMA_Root_Cause_Fix_Protocol.md
personal/PAMA_Runtime_Memory_Policy.md
```

## Update Workflow

### 1. Identify Installed State

Inspect the target Vault for:

```text
00-Core/
80-Indexes/
81-Dashboards/
90-Drafts/
91-Inbox/
92-Logs/
93-Proposals/
99-Archive/
```

Then read any installed version markers:

```text
00-Core/Installed-Memory-Architecture.md
00-Core/Core-Document-Index.md
00-Core/Core-Memory.md
80-Indexes/Architecture-Index.md
80-Indexes/README.md
```

If no version marker exists, infer the version from Core filenames, index filenames, and changelogs.

### 2. Create a Cleanup Archive

Before moving or replacing active files, create:

```text
99-Archive/Updates/YYYY-MM-DD-v<target-version>-update/
```

Inside it, create:

```text
snapshot-before-update/
deprecated-active-files/
```

Copy active files that will be touched into `snapshot-before-update/`.

Move superseded active files into `deprecated-active-files/`.

Do not move logs, raw records, decisions, or existing archive files unless the user explicitly asks.

### 3. Sync Current Core Files

For ARMOR, active Core should include:

```text
00-Core/ARMOR-V7.2-Stable.md
00-Core/Governance-Patch-V715.md
00-Core/Agent-Runtime-Adaptation-Guide.md
00-Core/Multi-Agent-Shared-Vault-Governance.md
00-Core/Prompt-Intake-Router.md
00-Core/Memory-Write-Router.md
00-Core/Root-Cause-Fix-Protocol.md
00-Core/Runtime-Memory-Policy.md
00-Core/Permission-Policy.md
00-Core/Retrieval-Rules.md
00-Core/Source-of-Truth-Map.md
00-Core/Installed-Memory-Architecture.md
00-Core/Core-Document-Index.md
```

For PAMA, active Core should include the PAMA equivalents:

```text
00-Core/PAMA V5.3 Stable.md
00-Core/PAMA_Multi_Agent_Shared_Vault_Governance.md
00-Core/PAMA_Prompt_Intake_Router.md
00-Core/PAMA_Memory_Write_Router.md
00-Core/PAMA_Root_Cause_Fix_Protocol.md
00-Core/PAMA_Runtime_Memory_Policy.md
```

Preserve Vault-local policies that are still valid, but update their references to current active files.

### 4. Sync Active Indexes

Active indexes should point to the current architecture.

For ARMOR v1.2.2 / V7.2, prefer:

```text
80-Indexes/Architecture-Index.md
80-Indexes/README.md
```

Archive old active indexes such as:

```text
80-Indexes/V7-1-Index.md
80-Indexes/V7-2-draft-index.md
```

Do not leave old version indexes in active `80-Indexes/` unless they are clearly marked `status: historical` and excluded from default retrieval.

### 5. Clean Active References

Search only active truth and navigation layers first:

```text
00-Core/
01-Facts/
02-Rules/
03-Insights/
04-Research/01-Reviewed/
05-Projects/
80-Indexes/
81-Dashboards/
```

Look for retired filenames, retired tools, and old version labels.

Examples:

```text
Claudian
Hermes-V71-Adaptation-Guide
Hermes-Operating-Protocol
Profile-Skills-Architecture
V7.1 Stable
AI Agent Memory Architecture v1.1.0
PAMA Personal V5.2
```

Classify each hit:

| Hit Location | Default Action |
| --- | --- |
| Active Core current rule | Update or replace |
| Active Index | Update or archive |
| Active Fact or Rule | Update only if it claims current truth |
| Active Project | Update if it controls ongoing work |
| Pending Proposal targeting retired files | Mark superseded or retarget |
| Log | Preserve |
| Raw Record | Preserve |
| Decision Record | Preserve, optionally add a superseded note |
| Archive | Preserve |

### 6. Mark Superseded Proposals

If a pending proposal references retired active files, do not silently execute it.

Either:

- update its target to current files if the proposal is still valid
- mark it `status: superseded` if the migration has already been completed or the target architecture changed

Recommended note:

```text
Superseded on YYYY-MM-DD by AI Agent Memory Architecture vX.Y.Z / <branch version>.
Retained as historical migration context only. Do not execute old target paths.
Current active entry points are: <list current files>.
```

### 7. Preserve Historical Evidence

Do not rewrite these just because they mention old tools or versions:

```text
06-Records/
92-Logs/
99-Archive/
historical decisions
completed proposals
```

Old terms in these locations are evidence of what happened at the time.

Only add a superseded note when a historical file is likely to be mistaken for current instructions.

### 8. Write an Update Log

For ARMOR shared Vaults, use the agent namespace:

```text
92-Logs/{Agent-Name}/YYYY-MM-DD-architecture-update.md
```

For PAMA shared Vaults, use the configured PAMA agent log or review namespace.

The update log should include:

- source repository and target version
- files added
- files replaced
- files archived
- proposals marked superseded
- validation results
- remaining known historical references

### 9. Validate

Run these checks:

```text
1. Required current Core files exist.
2. Active indexes point to the current architecture.
3. Retired active filenames are absent from active truth layers, except in explicit "archived/superseded" notes.
4. Runtime memory is not described as long-term memory.
5. Logs, records, and archives were not rewritten to erase history.
6. Agent namespaces exist when the Vault is shared by multiple agents.
7. Pending proposals do not target retired active files.
8. Update log exists.
```

## Version-Specific Cleanup Notes

### v1.2.2 / ARMOR Enterprise V7.2 Stable

Current active replacements:

| Old Active File or Concept | Current Replacement | Action |
| --- | --- | --- |
| `00-Core/Hermes-V71-Adaptation-Guide.md` | `00-Core/Agent-Runtime-Adaptation-Guide.md` | Archive old active file |
| `00-Core/Hermes-Operating-Protocol.md` | Generic routers + runtime adaptation + multi-agent governance | Archive old active file |
| `00-Core/Profile-Skills-Architecture.md` | Runtime-local Hermes documentation, not ARMOR Core | Archive or move outside active Core |
| `80-Indexes/V7-1-Index.md` | `80-Indexes/Architecture-Index.md` | Archive old active index |
| Claudian or Obsidian UI executor plugin support | Direct trusted runtime file access | Archive old execution guides |
| `AI Agent Memory Architecture v1.1.0`, `v1.2.0`, or `v1.2.1` as current version | `AI Agent Memory Architecture v1.2.2` | Update active version markers |
| `PAMA Personal V5.2` as current version | `PAMA Personal V5.3 Stable` | Update active version markers |

Expected active ARMOR entry points:

```text
00-Core/Core-Document-Index.md
00-Core/Installed-Memory-Architecture.md
00-Core/Agent-Runtime-Adaptation-Guide.md
00-Core/Multi-Agent-Shared-Vault-Governance.md
80-Indexes/Architecture-Index.md
```

Retain historical mentions in:

```text
06-Records/
92-Logs/
99-Archive/
completed or superseded proposals
```

## Final Rule

An update is complete only when the active Vault points to the latest architecture and stale active files cannot be mistaken for current truth.

Clean active truth.

Preserve history.

Archive instead of erase.

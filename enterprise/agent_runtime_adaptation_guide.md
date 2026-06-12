# Agent Runtime Adaptation Guide

> Applies to: Hermes, Claude Code, Codex, Cline, OpenHands, Opencode, custom agents, MCP-backed agents, and other trusted runtimes with direct Vault file access.
>
> Goal: help any organization connect an AI agent runtime to ARMOR without letting runtime memory, caches, embeddings, drafts, raw records, or archives become authoritative business memory.

---

## 0. Core Principle

The runtime is not the memory architecture.

```text
Vault = durable memory / source of truth / audit layer
Agent runtime = capability layer / task execution / temporary state
Runtime memory = cache / session continuity / indexes / task state
```

The runtime may read, search, draft, patch, summarize, classify, and create files. Those capabilities do not grant authority. ARMOR's routers, permission model, retrieval policy, and proposal workflow decide what the runtime may write and what can become current truth.

---

## 1. Runtime Requirements

A runtime can operate an ARMOR Vault if it can:

- read Markdown files
- search file content and filenames
- create directories and files
- append records and logs
- patch existing files safely
- preserve existing user content
- distinguish temporary state from durable memory
- follow a router before persistent writes
- create proposals instead of silently editing high-authority files

Optional capabilities:

- semantic search
- metadata indexing
- schema validation
- scheduled review reminders
- subagents or tools for audits and dashboards

---

## 2. Required Boundaries

The runtime must treat these as temporary and low-authority:

- built-in memory
- SQLite or local databases
- Hindsight-style memory stores
- embeddings
- vector indexes
- retrieval caches
- session summaries
- tool execution metadata
- recent file lists

The runtime must not store these as authoritative runtime memory:

- core principles
- permission policy
- retrieval policy
- approved rules
- product facts
- brand facts
- customer current state
- business positioning
- security policy
- reviewed research as truth
- architecture decisions

If deleting the runtime database causes authoritative facts or rules to disappear, the deployment is misconfigured.

---

## 3. Recommended Runtime Configuration

Use this as a conceptual target. Adapt field names to the actual runtime.

```yaml
memory:
  long_term_memory:
    provider: markdown_vault
    path: "/path/to/ARMOR-Vault"
    role: source_of_truth
    authoritative: true

  runtime_memory:
    provider: local_cache
    path: ".agent-runtime/runtime.sqlite"
    role: runtime_cache
    authoritative: false
    clearable: true
    rebuildable_from_vault: true

  memory_tool:
    enabled: true
    mode: runtime_only
    authoritative: false
    may_store:
      - session_state
      - task_state
      - retrieval_cache
      - embedding_index
      - file_hashes
      - temporary_plans
      - tool_execution_metadata
    must_not_store:
      - core_principles
      - permission_policy
      - retrieval_rules
      - brand_facts
      - product_facts
      - customer_current_state
      - approved_rules
      - reviewed_research_as_truth
      - long_term_facts
```

If a runtime supports only one memory provider, choose the Vault as the long-term memory location and keep any database-like store as cache only.

If a runtime does not support a formal Vault memory provider, direct file read/search/write/patch access is sufficient. The important requirement is not a specific memory-provider API. The important requirement is that the runtime treats the Vault as durable memory and treats its own databases, embeddings, summaries, and indexes as temporary infrastructure.

---

## 4. Startup Instruction Template

Place an equivalent instruction in the runtime's system prompt, profile, skill, startup note, or operating protocol.

```markdown
# ARMOR Runtime Operating Protocol

You operate an ARMOR Enterprise AI Workspace Vault.

The Vault is the durable source of truth. Runtime memory, embeddings, indexes, and local databases are temporary infrastructure only.

Before persistent writes:
1. Classify the user's intent with `00-Core/Prompt-Intake-Router.md`.
2. If the user asks to remember something, use `00-Core/Memory-Write-Router.md`.
3. If the user reports an error or asks for a fix, use `00-Core/Root-Cause-Fix-Protocol.md`.
4. Check permission class before writing.
5. Search existing SSOT files before creating or updating authority files.
6. Write low-authority capture directly only where allowed.
7. Create a proposal for high-authority or conflicting changes.
8. In shared Vault deployments, follow `00-Core/Multi-Agent-Shared-Vault-Governance.md`.

Never treat drafts, inbox notes, raw records, logs, proposals, archives, runtime memory, or raw research as current truth by default.
```

---

## 5. Retrieval Presets

Default execution retrieval:

```text
00-Core/
01-Facts/
02-Rules/
03-Insights/
04-Research/01-Reviewed/
05-Projects/active project only
```

Default exclusions:

```text
90-Drafts/
91-Inbox/
92-Logs/
93-Proposals/
94-Review-Queues/
99-Archive/
04-Research/00-Inbox/
06-Records/ unless evidence mode is requested
```

Evidence retrieval may load `06-Records/`, but records remain evidence, not current facts.

Historical retrieval may load `99-Archive/`, but output must be marked historical and must not update current truth without proposal.

---

## 6. Write Policy

Allowed direct writes:

- drafts
- inbox notes
- execution logs
- raw records
- active project working files
- review queue entries
- proposals

In shared Vault deployments, direct writes should use agent-specific namespaces where applicable:

```text
91-Inbox/{agent-name}/
92-Logs/{agent-name}/
93-Proposals/{agent-name}/
```

Every runtime should have a stable `agent_name`. New files created by an agent should include `author_agent: {agent-name}` in frontmatter unless the target file format forbids frontmatter.

Proposal or explicit human approval required:

- `00-Core/`
- `01-Facts/`
- `02-Rules/`
- authority-changing edits to reviewed research or insights
- customer current state changes
- product or brand positioning changes
- permission, retrieval, lifecycle, security, or architecture changes

When unsure, store lower or create a proposal.

---

## 7. Runtime-Specific Notes

For shared Vault deployments where multiple runtimes operate the same ARMOR Vault, also follow `00-Core/Multi-Agent-Shared-Vault-Governance.md`. Each runtime should use agent-specific namespaces for inbox notes, logs, and proposals, and must not treat another agent's drafts, logs, proposals, raw records, or runtime cache as authoritative memory.

### Hermes

Hermes may use Hindsight, SQLite, or built-in memory for runtime continuity, but authoritative memory should live in the ARMOR Vault. Use Hermes memory tools as pointer/cache infrastructure unless the user has explicitly configured a governed Vault-backed memory provider.

### Claude Code / Opencode

Use direct file read/search/write/patch tools against the Vault. Do not create hidden memory stores that override the Vault. Log significant actions to `92-Logs/{agent-name}/` and create proposals for authority-changing edits under `93-Proposals/{agent-name}/` in shared Vault deployments.

### Codex

Codex should connect to ARMOR as a file-based trusted executor.

Recommended local setup:

```text
Codex reference:
  ~/.codex/memory/reference_armor_vault.md

Codex skill:
  ~/.codex/skills/armor-enterprise-vault/SKILL.md

Shared Vault:
  /path/to/ARMOR-Vault
```

The Codex reference should record the Vault path, role boundaries, default retrieval rules, write classes, and required routers. The Codex skill should tell future Codex sessions when to activate the ARMOR workflow and which core Vault files to read first.

Codex should treat its own local memory database, session history, logs, embeddings, and indexes as temporary runtime infrastructure. They may store task continuity or short pointers, but they must not store authoritative facts, rules, product truth, customer state, or architecture decisions as long-term memory.

In shared Vault deployments, Codex should use:

```text
91-Inbox/Codex/
92-Logs/Codex/
93-Proposals/Codex/
```

Codex-created Vault files should use `author_agent: Codex` when frontmatter is appropriate.

For shared Vault deployments, add the Vault path as a trusted Codex project when the user wants Codex to work there regularly:

```toml
[projects."/path/to/ARMOR-Vault"]
trust_level = "trusted"
```

Codex must still follow the ARMOR permission model. Trusted project access grants file capability, not authority to modify Class A memory directly.

### Cline / OpenHands / Custom Agents

Configure the workspace root to the Vault or expose the Vault as a controlled file root. Ensure the agent can search before writing and can create proposals instead of directly editing high-authority files.

---

## 8. Validation Tests

Run these tests after integration:

1. Delete or ignore runtime cache.
   - Expected: authoritative facts and rules still exist in the Vault.

2. Ask a current fact question.
   - Expected: runtime searches SSOT and approved rules before using drafts or records.

3. Ask the runtime to remember a long-term rule.
   - Expected: runtime activates Memory Write Router and creates a proposal if the rule is high-authority.

4. Ask the runtime to fix a wrong behavior.
   - Expected: runtime locates the source file or creates a fix proposal, not a runtime memory patch.

5. Ask an ambiguous command such as "update this".
   - Expected: runtime checks risk and asks a concise clarification question when persistence is unclear.

6. Ask two different runtimes to write task logs.
   - Expected: each runtime writes to its own `92-Logs/{agent-name}/` namespace.

7. Ask one runtime to use another runtime's proposal as current truth.
   - Expected: runtime refuses to treat the proposal as approved truth and searches approved layers instead.

---

## 9. Final Principle

ARMOR does not require a specific agent product.

Any trusted runtime may operate the Vault if it obeys the architecture:

```text
Capability does not grant authority.
Vault memory outranks runtime memory.
Uncertain information is stored lower.
Authority changes require review or proposal.
```

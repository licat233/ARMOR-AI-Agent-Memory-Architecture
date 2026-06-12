# ARMOR Memory Write Router

> Mandatory routing rules for user-requested permanent memory in ARMOR Enterprise AI Workspace.

Version: 1.0
Status: Stable
Applies To: trusted agent runtimes, ARMOR Enterprise AI Workspace
Depends On: V7.1 Stable + V7.1.5 Governance Patch

---

## Core Rule

When the user asks the agent runtime to remember something, the agent runtime must not write it to runtime memory by default.

Runtime memory is cache only. The Obsidian Vault is the only long-term memory and Source of Truth.

User prompts should reach this router through `00-Core/Prompt-Intake-Router.md`, which first determines whether the user intent is Remember, Fix, Discussion, Direct Task, Ambiguous, or High-Risk.

In ARMOR, "remember this" means:

```text
extract -> classify -> route -> write or propose in the Vault
```

It does not mean:

```text
store full content in built-in memory
```

Runtime memory may only store short pointers, temporary task state, caches, or retrieval indexes.

This router is only for user-requested memory. When the user reports an error or asks the agent runtime to fix a mistake, the agent runtime must activate `00-Core/Root-Cause-Fix-Protocol.md` instead of storing a memory patch.

---

## Trigger Phrases

This router must activate when the user uses phrases such as:

- remember this
- remember that
- add this to memory
- update your memory
- save this rule
- keep this as a rule
- remember this going forward
- use this rule going forward
- make this the standard
- keep this for future work

Equivalent intent matters more than exact wording.

---

## Write Flow

Before storing any user-requested memory, the agent runtime must:

1. Extract the memory candidate.
2. Classify the information type.
3. Identify the source and confidence label.
4. Decide whether the memory is runtime-only, Vault capture, Vault authority, or proposal-required.
5. Search existing SSOT files when the target is authoritative.
6. Write to the correct Vault location or create a proposal.
7. Store only a short pointer in runtime memory if a pointer is useful.

If the agent runtime is unsure where to store the memory, it must not use runtime memory as fallback.

Fallback location:

```text
91-Inbox/Memory-Candidates/
```

---

## Runtime Memory Prohibition

The agent runtime must not store the following as full content in runtime memory:

- core principles
- permission rules
- retrieval rules
- approved rules
- long-term user preferences
- business facts
- brand facts
- product facts
- customer current state
- project decisions
- architecture decisions
- SOPs
- security policy

Allowed runtime memory content:

- session state
- current task state
- retrieval cache
- embedding index
- temporary plan state
- short pointer to a Vault file

---

## Routing Table

| User-requested memory type | Correct destination | Notes |
| --- | --- | --- |
| Core principles, architecture principles, permission policy, retrieval policy | `93-Proposals/Core/` -> `00-Core/` | Class A. Proposal required. |
| Agent runtime behavior rules and operating protocol changes | `93-Proposals/Core/` -> `00-Core/Agent-Operating-Protocol.md` | Class A. Proposal required. |
| Execution rules, writing rules, SOPs, content standards | `93-Proposals/Rules/` -> `02-Rules/` | Class A. Proposal required for authoritative rules. |
| Brand facts, product facts, customer facts, company positioning | `93-Proposals/Facts/` -> `01-Facts/` | Search SSOT first. |
| Project state, task plans, phase progress | `05-Projects/{project}/` | Class B when scoped to active work. |
| Validated lessons, success or failure patterns, postmortems | `03-Insights/` | Require evidence and source. |
| Meetings, raw conversations, customer feedback, source evidence | `06-Records/` | Append-only evidence, not current fact by default. |
| External research, market notes, competitor information | `04-Research/00-Inbox/` | Reviewed research may later move to `04-Research/01-Reviewed/`. |
| Unclear, weak, or unclassified memory candidates | `91-Inbox/Memory-Candidates/` | Never runtime memory fallback. |
| Draft ideas or unapproved working material | `90-Drafts/` | Low authority. |
| High-authority change needing human review | `93-Proposals/` | Do not directly edit authority file. |
| Temporary task state or current session continuity | runtime memory | Short-lived only. |

---

## Examples

### Rule Request

User:

```text
Remember: all company website articles must start with SEO structure planning before drafting the body.
```

The agent runtime should classify:

```yaml
type: rule
target_class: Class A
destination: 93-Proposals/Rules/
final_authority: 02-Rules/Content/
runtime_memory: short pointer only
```

The agent runtime should not reply with only:

```text
Saved to memory.
```

### Architecture Decision

User:

```text
Remember: Supermemory is not part of the formal architecture for now; treat it only as an observation target.
```

The agent runtime should classify:

```yaml
type: architecture_decision
target_class: Class A or B depending on impact
destination: 93-Proposals/Core/ or 03-Insights/AI-Memory-Architecture/
runtime_memory: short pointer only
```

### Customer Visit Record

User:

```text
Remember: the customer representative visited the company and discussed requirements for a new project.
```

The agent runtime should classify:

```yaml
type: record
target_class: Class R
destination: 06-Records/Customers/
runtime_memory: short pointer only
```

If the visit changes the customer's current state, the agent runtime should create a proposal for `01-Facts/Customers/`.

---

## Required Response Pattern

When the agent runtime routes a memory request, it should report:

```text
Memory classified as: {type}
Destination: {vault path}
Authority: {runtime-only | capture | authority | proposal-required}
Runtime memory: {not used | pointer only}
```

For Class A changes, the agent runtime must say that it created or will create a proposal rather than silently modifying the authority file.

---

## Final Principle

In ARMOR, "remember" is a governed Vault write action.

In ARMOR, "fix this" is a Root-Cause Fix Protocol event.

Runtime memory is not long-term memory.

Unclear memory goes to `91-Inbox/Memory-Candidates/`, never to runtime memory by default.

# PAMA Multi-Agent Shared Vault Governance

> Governance policy for multiple trusted agent runtimes operating on one shared PAMA Personal Vault.

Version: 1.0
Status: Stable
Applies To: PAMA V5.2 Stable, trusted agent runtimes, AI assistants, Hermes, Claude Code, Codex, Opencode, Cline, OpenHands, custom agents
Depends On: PAMA V5.2 Stable + PAMA Constitution + PAMA Deployment Spec + PAMA Prompt Intake Router + PAMA Memory Write Router + PAMA Root-Cause Fix Protocol + PAMA Runtime Memory Policy

---

## Purpose

A personal memory Vault can be shared by multiple trusted agents only when every agent respects user sovereignty, PAMA layer authority, and strict promotion rules.

This policy prevents agents from overwriting each other, treating another agent's interpretation as personal truth, duplicating memory, or leaking runtime cache into durable personal memory.

---

## Core Principle

Multiple agents may help operate one PAMA Vault.

Only the user has final authority over durable personal truth.

The Vault is durable memory.

Agents are execution runtimes.

Runtime memory is temporary cache only.

Agent-created memory is low-authority by default unless routed, reviewed, and accepted through PAMA governance.

```text
PAMA Vault = durable personal memory / review layer
User = final authority
Agent runtime = executor and reviewer
Runtime memory = temporary cache
```

---

## Primary Risks

| Risk | Description | Required Control |
| --- | --- | --- |
| Self-model pollution | An agent writes a hypothesis as identity or durable truth | Store in `06-Meta/` or `08-Working-Memory/`, review before promotion |
| Truth inflation | Passing preferences become permanent `05-Truth/` entries | Truth requires repeated evidence or user confirmation |
| Agent interpretation drift | One agent's summary becomes another agent's fact | Conservative retrieval and frontmatter authority |
| Goal hijacking | An agent modifies goals or priorities without approval | Confirm or queue review for `04-Goals/` changes |
| Decision contamination | An agent rewrites decision records or expected outcomes | Append feedback or create review item, do not silently rewrite |
| Runtime backflow | Runtime memory becomes durable personal memory | Runtime memory policy and memory write router |
| Write conflict | Multiple agents edit the same personal note | Agent namespaces and conflict notes |

---

## Agent Namespaces

Agents should not mix uncertain working material in shared flat folders.

Recommended namespaced locations:

```text
08-Working-Memory/
  Codex/
  Hermes/
  Claude-Code/
  Memory-Candidates/
    Codex/
    Hermes/
    Claude-Code/
  Fix-Candidates/
    Codex/
    Hermes/
    Claude-Code/

07-Reviews/
  Codex/
  Hermes/
  Claude-Code/
  Promotion-Candidates/
  Conflict-Reviews/
```

Optional execution logs:

```text
08-Working-Memory/Logs/Codex/
08-Working-Memory/Logs/Hermes/
08-Working-Memory/Logs/Claude-Code/
```

Additional agents should use stable, human-readable names:

```text
08-Working-Memory/Opencode/
08-Working-Memory/Cline/
08-Working-Memory/OpenHands/
```

---

## High-Authority Personal Memory Boundary

Agents must not directly edit these high-authority personal layers unless the user explicitly approves the exact edit:

```text
00-Core/
05-Truth/
```

Agents must treat these layers as high-risk when the edit changes meaning, priority, or future behavior:

```text
03-Decisions/
04-Goals/
```

Default targets for high-risk or authority-changing changes:

```text
07-Reviews/Promotion-Candidates/
07-Reviews/Conflict-Reviews/
08-Working-Memory/Memory-Candidates/{agent-name}/
08-Working-Memory/Fix-Candidates/{agent-name}/
```

No agent may promote material into `05-Truth/` without user approval or an explicit review decision.

---

## Required Frontmatter

Every new agent-created PAMA file should include frontmatter unless the target file format forbids it.

Recommended minimum:

```yaml
---
author_agent: Codex
created_at: 2026-06-12
source_type: user_request | agent_observation | document | conversation | review | tool_output
source_ref:
confidence: high | medium | low
authority: low | medium | high
status: working | candidate | review | approved | archived
target_layer: 08-Working-Memory
review_required: false
user_confirmed: false
---
```

For truth candidates, also include:

```yaml
truth_candidate: true
evidence_count:
contradicting_evidence:
review_gate: weekly | monthly | explicit_user_approval
```

For goal or decision changes, also include:

```yaml
change_type: goal_update | decision_update | decision_feedback | priority_change
review_owner: user
decision: pending
```

---

## Retrieval Rules

All agents must use conservative retrieval by default.

Default current personal-memory sources:

```text
00-Core/
01-Reality/
03-Decisions/
04-Goals/
05-Truth/
07-Reviews/ relevant approved reviews only
```

Conditional sources:

```text
02-Attention/ when reviewing behavior, alignment, priorities, or energy use
06-Meta/ only when hypotheses or self-models are explicitly relevant
08-Working-Memory/ only for current task continuity or candidate review
99-Archive/ only for explicit historical recall
```

Default exclusions:

```text
06-Meta/ as current reality
08-Working-Memory/ as durable truth
07-Reviews/ unapproved review drafts
99-Archive/ as current truth
runtime memory
other agents' working notes, logs, candidates, or interpretations
```

No agent may treat another agent's working note, hypothesis, review draft, candidate, log, or runtime cache as authoritative personal memory.

---

## Write Routing

All agents must use the same PAMA routing rules:

| User intent | Required route |
| --- | --- |
| Remember this | `00-Core/PAMA-Memory-Write-Router.md` |
| Fix this / this is wrong | `00-Core/PAMA-Root-Cause-Fix-Protocol.md` |
| Ambiguous short command | `00-Core/PAMA-Prompt-Intake-Router.md` |
| Runtime memory question | `00-Core/PAMA-Runtime-Memory-Policy.md` |

No runtime may use its own memory feature as a shortcut around these routes.

---

## Conflict Policy

Agents should avoid editing the same personal memory file concurrently.

Preferred write pattern:

```text
08-Working-Memory/{agent-name}/YYYY-MM-DD-topic.md
08-Working-Memory/Memory-Candidates/{agent-name}/YYYY-MM-DD-topic.md
07-Reviews/{agent-name}/YYYY-MM-DD-review-note.md
07-Reviews/Conflict-Reviews/YYYY-MM-DD-file-conflict.md
```

Before modifying an existing file, the agent must:

1. Read the latest file content.
2. Identify the exact section to patch.
3. Check whether the edit changes truth, goals, decisions, or identity claims.
4. Apply the smallest safe patch only when permitted.
5. Stop and create a conflict review if the file changed in a way that may affect the edit.

Conflict review minimum content:

```yaml
---
author_agent: Codex
status: review
review_required: true
target_file:
conflict_detected_at: 2026-06-12
user_decision_required: true
---
```

```text
Observed conflict:
Potential impact on personal truth, goals, decisions, or reality:
Recommended resolution:
```

---

## Agent Role Model

Example role split:

| Agent | Default Role | Default Write Zone |
| --- | --- | --- |
| Hermes | Primary daily personal memory operator | `08-Working-Memory/Hermes/`, approved PAMA paths |
| Codex | Architecture, repo, documentation, and structured patch executor | `08-Working-Memory/Codex/`, `07-Reviews/Codex/` |
| Claude Code | Secondary executor and reviewer | `08-Working-Memory/Claude-Code/`, `07-Reviews/Claude-Code/` |
| User | Final authority over personal truth, goals, and identity claims | Approval and review decisions |

This role model can be adapted, but one rule is fixed:

```text
No agent is automatically the final authority for personal truth.
```

---

## Review Cadence

Recommended cadence:

| Area | Review Action | Frequency |
| --- | --- | --- |
| `08-Working-Memory/Memory-Candidates/` | Classify, promote to review, or archive | Weekly |
| `08-Working-Memory/Fix-Candidates/` | Resolve source fixes or create review item | Weekly |
| `06-Meta/` | Validate, decay, demote, or archive hypotheses | Monthly |
| `02-Attention/` | Compare stated priorities with actual attention | Weekly or monthly |
| `03-Decisions/` | Add feedback and outcome evidence | Monthly or decision-specific |
| `04-Goals/` | Check alignment and update only with user approval | Weekly or monthly |
| `05-Truth/` | Keep small; promote rarely after review | Monthly or explicit approval |

Review outputs should be recorded in:

```text
07-Reviews/
07-Reviews/Promotion-Candidates/
07-Reviews/Conflict-Reviews/
```

---

## Installation Requirements

When installing PAMA for a multi-agent personal workspace, create these directories in addition to the standard PAMA structure:

```text
08-Working-Memory/Codex/
08-Working-Memory/Hermes/
08-Working-Memory/Claude-Code/
08-Working-Memory/Memory-Candidates/Codex/
08-Working-Memory/Memory-Candidates/Hermes/
08-Working-Memory/Memory-Candidates/Claude-Code/
08-Working-Memory/Fix-Candidates/Codex/
08-Working-Memory/Fix-Candidates/Hermes/
08-Working-Memory/Fix-Candidates/Claude-Code/
08-Working-Memory/Logs/Codex/
08-Working-Memory/Logs/Hermes/
08-Working-Memory/Logs/Claude-Code/
07-Reviews/Codex/
07-Reviews/Hermes/
07-Reviews/Claude-Code/
07-Reviews/Promotion-Candidates/
07-Reviews/Conflict-Reviews/
```

These are starter namespaces only. Add or remove agent namespaces according to the actual deployment.

---

## Validation Tests

Run these tests after multi-agent setup:

1. Ask one agent to remember a durable personal preference.
   - Expected: it writes a candidate or review item, not a direct `05-Truth/` edit.

2. Ask another agent to answer from current personal truth.
   - Expected: it retrieves approved `05-Truth/` and relevant evidence, not the first agent's candidate note.

3. Ask two agents to write working notes.
   - Expected: each writes to its own `08-Working-Memory/{agent-name}/` namespace.

4. Ask an agent to treat a hypothesis as reality.
   - Expected: it refuses and distinguishes `06-Meta/` from `01-Reality/`.

5. Ask an agent to change goals or major decisions.
   - Expected: it asks for confirmation or creates a review item.

6. Simulate a file conflict.
   - Expected: the agent stops and writes a conflict review under `07-Reviews/Conflict-Reviews/`.

---

## Final Principle

PAMA shared Vault memory is safe only when the user remains the final authority and agent-created material stays correctly layered.

```text
No agent may treat another agent's working note, hypothesis, review draft, candidate, log, or runtime cache as authoritative personal memory.

Only user-approved or properly reviewed PAMA layers may serve as durable personal truth.
```

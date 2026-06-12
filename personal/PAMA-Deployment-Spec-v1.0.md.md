# PAMA Deployment Spec v1.0

## Implementation Specification For PAMA V5.1 Stable

Version: 1.0
Status: Stable
Depends On:

- PAMA-V5.1-Stable.md
- PAMA-Constitution-v1.0.md
- PAMA-Prompt-Intake-Router.md
- PAMA-Memory-Write-Router.md
- PAMA-Root-Cause-Fix-Protocol.md
- PAMA-Runtime-Memory-Policy.md

Priority:

```text
Constitution
    >
PAMA Stable
    >
Deployment Spec
    >
Prompt Intake Router
    >
Memory Write Router
    >
Root-Cause Fix Protocol
    >
Runtime Memory Policy
```

Purpose:

This document defines how a trusted agent runtime must physically deploy, operate, maintain, and evolve a PAMA-based memory system.

------

# 1. Deployment Objectives

The agent runtime must build a system that is:

- Stable
- Low-maintenance
- Human-readable
- Future-proof
- Obsidian-compatible
- AI-friendly

The system must remain usable even if all AI tools disappear.

Markdown remains the primary storage format.

------

# 2. Vault Structure

Create the following structure.

```text
Personal-Vault/

├── 00-Core/
│   ├── PAMA-V5.1-Stable.md
│   ├── PAMA-Constitution-v1.0.md
│   ├── PAMA-Deployment-Spec-v1.0.md
│   ├── PAMA-Prompt-Intake-Router.md
│   ├── PAMA-Memory-Write-Router.md
│   ├── PAMA-Root-Cause-Fix-Protocol.md
│   ├── PAMA-Runtime-Memory-Policy.md
│   ├── Principles.md
│   ├── Long-Term-Goals.md
│   └── Operating-Rules.md
│
├── 01-Reality/
│   ├── Events.md
│   ├── Outcomes.md
│   └── Metrics.md
│
├── 02-Attention/
│   └── Attention-Log.md
│
├── 03-Decisions/
│   ├── Decision-Records.md
│   └── Lessons.md
│
├── 04-Goals/
│   └── Goal-Market.md
│
├── 05-Truth/
│   ├── Principles/
│   ├── Knowledge/
│   ├── Frameworks/
│   └── Preferences/
│
├── 06-Meta/
│   └── Hypotheses.md
│
├── 07-Reviews/
│   ├── Weekly/
│   ├── Monthly/
│   └── Quarterly/
│
├── 08-Working-Memory/
│
└── 99-Archive/
```

No additional folders should be created without user approval.

------

# 3. Default Memory Routing

The agent runtime must determine destination before writing.

Before routing memory, fixes, or persistent changes, the agent runtime must pass user prompts through `00-Core/PAMA-Prompt-Intake-Router.md` to classify intent, risk, and persistence level.

When the user explicitly asks the assistant to "remember" something, the agent runtime must treat that request as a Memory Write Router event, not as a default runtime memory write.

Runtime memory is temporary cache only. User-requested permanent memory must be classified and routed to the Vault through `00-Core/PAMA-Memory-Write-Router.md`.

When the user reports an error or asks the assistant to fix a mistake, the agent runtime must not treat the correction as a memory write. It must activate `00-Core/PAMA-Root-Cause-Fix-Protocol.md`.

Runtime memory restrictions are governed by `00-Core/PAMA-Runtime-Memory-Policy.md`.

## Default

```text
Conversation
↓
08-Working-Memory
```

When uncertain:

Store lower.

Never store higher.

If the agent runtime cannot confidently classify a user-requested memory, the fallback is:

```text
08-Working-Memory/Memory-Candidates/
```

The fallback must not be runtime memory.

## Root-Cause Fix Routing

Fix requests follow a separate protocol:

```text
User reports error
↓
Agent runtime identifies source layer
↓
Agent runtime edits source or creates review item
↓
Agent runtime removes conflicting memory if memory caused the error
↓
Agent runtime writes repair log
↓
Agent runtime verifies behavior
```

Do not patch broken instructions with memory. Fix the broken instruction.

If the source of an error is editable, the agent runtime must edit the source. If it is not editable, the agent runtime must create a review item or fix note. Memory is not an acceptable substitute.

------

## Direct Reality

Examples:

- Project completed
- Goal achieved
- Product launched
- Important failure
- Significant life event

Destination:

```text
01-Reality/
```

------

## Direct Decision

Examples:

- Tool selection
- Major purchase
- Career choice
- Strategic change

Destination:

```text
03-Decisions/
```

------

## Direct Truth

Allowed only when:

- User explicitly requests
- Information repeatedly confirmed
- Long-term durable value exists

Destination:

```text
05-Truth/
```

------

# 4. Required Frontmatter

All new memory items should include:

```yaml
---
created:
updated:
type:
confidence:
source:
status:
---
```

------

# 5. Memory Types

Allowed types:

```yaml
type:
  reality
  decision
  goal
  truth
  lesson
  hypothesis
  review
  note
```

------

# 6. Confidence Levels

Allowed values:

```yaml
confidence:
  high
  medium
  low
```

Definitions:

High

- User confirmed
- Direct observation
- Verified fact

Medium

- Strong evidence
- Repeated pattern

Low

- Inference
- Interpretation
- Hypothesis

------

# 7. Reality Template

Template:

```yaml
---
type: reality
created:
updated:
confidence: high
source:
status: active
---

# Event

# Outcome

# Evidence

# Notes
```

Reality entries must avoid interpretation.

Only record observable facts.

------

# 8. Decision Template

Template:

```yaml
---
type: decision
created:
updated:
confidence: high
source:
status: active
---

# Context

# Alternatives

# Reason

# Prediction

# Outcome

# Lesson
```

Prediction is mandatory.

Outcome can be added later.

------

# 9. Goal Template

Template:

```yaml
---
type: goal
created:
updated:
status: active
---

# Goal

# Current Weight

# Evidence

# Notes
```

Goal weights should reflect observed behavior.

Not stated intentions.

------

# 10. Truth Template

Template:

```yaml
---
type: truth
created:
updated:
confidence: high
source:
status: active
---

# Statement

# Evidence

# Why It Matters

# Last Verification
```

Truth entries must remain concise.

Truth is not a knowledge dump.

------

# 11. Hypothesis Template

Template:

```yaml
---
type: hypothesis
created:
updated:
confidence:
status: active
---

# Hypothesis

# Evidence

# Counter Evidence

# Review Date
```

All hypotheses are temporary.

------

# 12. Writing Rules

Before writing:

The agent runtime must ask:

1. Is this reality?
2. Is this interpretation?
3. Is this temporary?
4. Is this durable?
5. Does evidence exist?
6. Which layer should own this?

If uncertain:

Store in Working Memory.

If the user says "remember", "save to memory", "use this rule going forward", or an equivalent phrase:

1. Activate `00-Core/PAMA-Memory-Write-Router.md`.
2. Do not store the full content in runtime memory.
3. Classify and route the memory to the correct Vault layer.
4. Use `08-Working-Memory/Memory-Candidates/` as the fallback when classification is unclear.
5. Store only a short pointer in runtime memory if needed.

If the user reports an error, says "fix this", "this is wrong", "repair this issue", or an equivalent phrase:

1. Activate `00-Core/PAMA-Root-Cause-Fix-Protocol.md`.
2. Identify the source layer of the error.
3. Fix the source directly if allowed.
4. If the source cannot be edited, create a review item or fix note.
5. Do not store a memory patch as a substitute.

------

# 13. Promotion Rules

Promotion path:

```text
Working Memory
↓
Review
↓
Truth
```

Required conditions:

- Repeated evidence
- Long-term value
- User approval OR strong confirmation

Never promote assumptions.

------

# 14. Demotion Rules

Allowed:

```text
Truth
↓
Hypothesis

Truth
↓
Archive

Meta
↓
Archive
```

Reasons:

- Contradictory evidence
- Expiration
- Obsolescence
- User request

------

# 15. Meta Decay Rules

Every hypothesis must contain:

```yaml
review_date:
```

Review schedule:

Low confidence

- 30 days

Medium confidence

- 90 days

High confidence

- 180 days

Expired hypotheses should be:

- Updated
- Downgraded
- Archived

------

# 16. Weekly Review

Generate:

```text
Weekly Review
```

Include:

- Important events
- Key decisions
- Attention distribution
- Emerging patterns
- Potential promotions

Store in:

```text
07-Reviews/Weekly/
```

------

# 17. Monthly Review

Include:

- Goal alignment
- Decision quality
- Reality vs expectations
- Attention shifts
- Hypothesis validation

Store in:

```text
07-Reviews/Monthly/
```

------

# 18. Quarterly Review

Include:

- Major life trajectory changes
- Long-term trend analysis
- Goal recalibration
- Truth verification
- Archive candidates

Store in:

```text
07-Reviews/Quarterly/
```

------

# 19. Archive Rules

Archive when:

- No longer useful
- Invalidated
- Superseded
- Expired

Move to:

```text
99-Archive/
```

Do not delete immediately.

Archive first.

Delete later if necessary.

------

# 20. Operational Priorities

Priority order:

```text
Reality
>
Attention
>
Decision
>
Goal
>
Truth
>
Meta
```

If conflict exists:

Higher priority wins.

------

# 21. Deployment Checklist

After deployment the agent runtime must verify:

✓ Directory structure created

✓ Core documents installed

✓ Prompt intake router installed

✓ Memory write router installed

✓ Root-cause fix protocol installed

✓ Runtime memory policy installed

✓ Templates created

✓ Review system established

✓ Promotion rules configured

✓ Archive rules configured

✓ Meta decay configured

✓ Exploration budget configured

✓ Initial review schedule configured

Deployment complete only after all checks pass.

------

# Final Rule

PAMA is not a database.

PAMA is not a note collection.

PAMA is a system for understanding reality and improving decisions over time.

Whenever uncertain:

Store lower.

Require evidence.

Review later.

Protect truth.

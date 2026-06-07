# PAMA Deployment Spec v1.0

## Implementation Specification For PAMA V5.1 Stable

Version: 1.0
Status: Stable
Depends On:

- PAMA-V5.1-Stable.md
- PAMA-Constitution-v1.0.md

Priority:

```text
Constitution
    >
PAMA Stable
    >
Deployment Spec
```

Purpose:

This document defines how Hermes must physically deploy, operate, maintain, and evolve a PAMA-based memory system.

------

# 1. Deployment Objectives

Hermes must build a system that is:

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

Hermes must determine destination before writing.

## Default

```text
Conversation
↓
08-Working-Memory
```

When uncertain:

Store lower.

Never store higher.

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

Hermes must ask:

1. Is this reality?
2. Is this interpretation?
3. Is this temporary?
4. Is this durable?
5. Does evidence exist?
6. Which layer should own this?

If uncertain:

Store in Working Memory.

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

After deployment Hermes must verify:

✓ Directory structure created

✓ Core documents installed

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
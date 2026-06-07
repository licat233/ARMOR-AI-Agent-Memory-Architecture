# PAMA V5.1 Stable

## Personal AI Memory Architecture

Version: 5.1 Stable
Status: Production Ready
Target: Personal AI Agent Systems
Designed For: Hermes, Claude Code, Cline, OpenHands, AI Assistants

------

# Mission

PAMA is not a note-taking system.

PAMA is not a personal knowledge management system.

PAMA is not a productivity system.

PAMA is:

> A Personal Reality, Decision, and Evolution Operating System.

Its purpose is to help the user:

- Understand reality
- Make better decisions
- Track personal evolution
- Preserve long-term truth
- Avoid self-deception
- Build a coherent life narrative

------

# Core Philosophy

Reality matters more than stories.

Behavior matters more than declarations.

Attention reveals priorities.

Decisions shape trajectories.

Truth should remain rare.

Identity is a temporary model.

The user is always changing.

The memory system must change too.

------

# Architecture Overview

```text
Conversation
      │
      ▼

Working Memory
(LLM Wiki)

      │
      ▼

Reality Layer

      │
      ▼

Attention Layer

      │
      ▼

Decision Layer

      │
      ▼

Goal Layer

      │
      ▼

Truth Layer
(Obsidian)

      │
      ▼

Meta Layer
(Hypotheses Only)
```

------

# Layer 0 — Conversation

Purpose:

Current interaction only.

Examples:

- Questions
- Casual discussion
- Temporary context
- Short-lived tasks

Retention:

Conversation lifetime.

Default behavior:

Do not store automatically.

------

# Layer 1 — Working Memory

Purpose:

Capture information before evaluation.

Examples:

- Ideas
- Learning notes
- Research
- Reading summaries
- Drafts
- Observations
- AI-generated insights

Characteristics:

- High volume
- Low friction
- Imperfect quality allowed

Default write destination.

When uncertain:

Store here.

------

# Layer 2 — Reality Layer

Purpose:

Record what actually happened.

Reality is the foundation of the entire system.

Examples:

- Project outcomes
- Business results
- Experiments
- Commitments completed
- Commitments failed
- Important events

Required fields:

```yaml
event:
date:
outcome:
evidence:
```

Reality must be evidence-based.

Avoid interpretation.

Avoid explanation.

Record only observable outcomes.

------

# Layer 3 — Attention Layer

Purpose:

Track where time and attention are invested.

Attention reveals actual priorities.

More reliable than stated intentions.

Examples:

```yaml
period:
AI:
Business:
Health:
Relationships:
Learning:
Entertainment:
```

Goal:

Identify attention drift.

Identify neglected areas.

Reveal true priorities.

------

# Layer 4 — Decision Layer

Purpose:

Preserve important decisions.

A decision is valuable even when it fails.

Required fields:

```yaml
decision:
date:
context:
alternatives:
reason:
prediction:
outcome:
lesson:
```

Goal:

Build a history of decision-making quality.

Improve future judgment.

------

# Layer 5 — Goal Layer

Purpose:

Track long-term drivers.

Goals are dynamic.

Goals compete.

Goals evolve.

Recommended structure:

```yaml
goals:

freedom:
weight:

health:
weight:

wealth:
weight:

creation:
weight:

relationships:
weight:
```

Weights represent actual importance.

Review regularly.

Update based on behavior.

Not based on declarations.

------

# Layer 6 — Truth Layer

Purpose:

Store durable truth.

Truth should remain small.

Truth should remain valuable.

Truth should remain trustworthy.

Examples:

- Personal principles
- Stable preferences
- Proven workflows
- Long-term knowledge
- Confirmed facts
- Reusable frameworks

Truth is expensive.

Do not store casually.

------

# Layer 7 — Meta Layer

Purpose:

Store current models.

Not truth.

Not identity.

Not facts.

Only hypotheses.

Example:

```yaml
hypothesis:
confidence:
evidence:
last_review:
```

Example:

```yaml
hypothesis:
  User currently prioritizes freedom over stability

confidence:
  0.78

evidence:
  - autonomous systems
  - preference for leverage
  - repeated behavior patterns
```

Meta Layer never overrides Reality.

Meta Layer never overrides Truth.

------

# Temporal Engine

Purpose:

Observe change over time.

Not a storage layer.

A system process.

Responsibilities:

- Detect trend shifts
- Detect attention shifts
- Detect goal shifts
- Detect recurring patterns
- Detect stagnation
- Detect growth

Example:

```yaml
trend:

attention_shift:
  AI → Health

goal_shift:
  Wealth → Freedom

confidence:
  high
```

------

# Interpretation Layer

Purpose:

Separate outcome from explanation.

Required structure:

```yaml
event:
outcome:
interpretation:
confidence:
```

Rule:

Outcome ≠ Cause

Never confuse results with explanations.

Interpretations remain hypotheses.

------

# Meta Decay System

Purpose:

Prevent identity lock-in.

Every Meta hypothesis decays over time.

Without new evidence:

Confidence decreases.

Old models lose authority.

Archived when confidence becomes too low.

Goal:

Allow personal evolution.

Prevent outdated self-models.

------

# Exploration Budget

Purpose:

Prevent cognitive echo chambers.

Rule:

At least 10–20% of exploration should come from outside established interests.

Examples:

- New fields
- New perspectives
- Contradictory viewpoints
- Unrelated disciplines

Goal:

Increase serendipity.

Increase creativity.

Prevent stagnation.

------

# Recommended Vault Structure

```text
Personal-Vault/

├── 00-Core/
│   ├── PAMA-V5.1-Stable.md
│   ├── PAMA-Constitution-v1.0.md
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

------

# Promotion Rules

Allowed flow:

```text
Conversation
↓
Working Memory
↓
Review
↓
Truth Layer
```

Direct promotion is discouraged.

Exceptions:

- Explicit user instruction
- Critical fact
- Major life decision
- Core principle

------

# Review Cycles

Weekly:

- Working Memory review
- Reality review
- Attention review

Monthly:

- Goal review
- Decision review
- Meta review

Quarterly:

- Truth review
- Trajectory analysis
- Long-term adjustment

------

# Agent Operational Checklist

Before storing:

1. Is this worth remembering?
2. Is this reality or interpretation?
3. Is this temporary or durable?
4. Does evidence exist?
5. Is this truth or hypothesis?
6. Does it belong in Working Memory first?
7. Will it still matter in one year?

When uncertain:

Store lower.

Never promote uncertainty into truth.

------

# Final Principle

The purpose of memory is not accumulation.

The purpose of memory is clarity.

The purpose of clarity is better decisions.

The purpose of better decisions is a better life.

PAMA exists to help the user understand reality, learn from experience, and evolve intentionally over time.
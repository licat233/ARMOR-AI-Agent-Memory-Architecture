# PAMA Personal AI Memory Architecture

> Personal Reality, Decision, and Evolution Operating System for AI-assisted long-term memory.

PAMA is the personal branch of AI Agent Memory Architecture. It is designed for one human user and one or more trusted AI agents working inside a personal Obsidian Vault or Markdown knowledge base.

Its purpose is not to flatter the user or remember every passing thought. Its purpose is to preserve high-fidelity memory about reality, attention, decisions, goals, reviewed lessons, and durable personal truth.

**Current release:** PAMA V5.1 Stable

### Mission

PAMA helps an AI assistant counter common human failure modes:

- Self-flattering narratives that conflict with evidence.
- Stated priorities that do not match actual attention.
- Short-term impulses that overwrite long-term direction.
- Echo chambers, confirmation bias, and cognitive closure.
- False certainty created by promoting weak signals too early.

### Core Principles

| Principle | Meaning |
| --- | --- |
| **Reality > Narrative** | When user belief conflicts with evidence, evidence wins. |
| **Behavior > Declarations** | Actual attention and behavior reveal priorities more reliably than stated goals. |
| **Truth Is Expensive** | Durable truth should stay small, verified, and hard to promote into. |
| **Store Lower When Uncertain** | Uncertain material belongs in working memory or meta layers first. |
| **User Sovereignty** | The system may challenge, question, and advise, but the user keeps final authority. |

### Standard Personal Vault Structure

```text
Vault/
├── 00-Core/                  # PAMA constitution, stable architecture, deployment rules
├── 01-Reality/               # Objective events, metrics, outcomes, evidence-backed logs
├── 02-Attention/             # Time and energy audit; attention reveals real priority
├── 03-Decisions/             # Decision records, feedback, lessons learned
├── 04-Goals/                 # Long-term vectors and short-term tactical goals
├── 05-Truth/                 # Verified principles, durable preferences, personal SSOT
├── 06-Meta/                  # Hypotheses, interpretations, assumptions, decay-managed ideas
├── 07-Reviews/               # Weekly, monthly, quarterly reviews and promotion gates
├── 08-Working-Memory/        # High-write, low-authority workspace for uncertain memory
└── 99-Archive/               # Deprecated, superseded, expired, or explicitly recalled memory
```

Top-level folders are part of the architecture boundary. Add subfolders inside layers when needed, but do not let an AI agent redesign the top-level map without explicit user approval.

### Agent Execution Layer

PAMA can be operated by any trusted agent runtime with file read/search/write/patch capability, including Hermes, Claude Code, Codex, Opencode, Cline, OpenHands, and custom agents. The runtime is an executor, not a personal truth authority.

Use the runtime to read, search, create working notes, append reality evidence, create decision records, prepare review items, and write completion logs. Do not use the runtime to promote passing thoughts into `05-Truth/`, treat `06-Meta/` as reality, treat `08-Working-Memory/` as durable truth, or override user sovereignty.

Recommended relationship:

```text
PAMA defines memory governance.
A trusted runtime executes allowed Vault operations.
The user decides what becomes durable personal truth.
```

### Layer Map

| Directory | Cognitive Layer | Governance Role | Default Retrieval |
| --- | --- | --- | --- |
| `00-Core/` | Architecture core | Constitution, operating rules, deployment spec | Always high priority |
| `01-Reality/` | Empirical observation | What objectively happened, with evidence and metrics | High priority |
| `02-Attention/` | Attention audit | Where time and energy actually went | Conditional, mainly reviews |
| `03-Decisions/` | Decision tracking | Major choices, expected outcomes, later feedback | High priority for decisions |
| `04-Goals/` | Goal management | Long-term direction and short-term strategy | Standard |
| `05-Truth/` | Crystallized truth | Verified principles, durable preferences, personal SSOT | Highest priority |
| `06-Meta/` | Hypotheses and interpretation | Unproven models, assumptions, decaying ideas | Blocked by default |
| `07-Reviews/` | Periodic review | Promotion, demotion, alignment reports | Conditional |
| `08-Working-Memory/` | Working memory | Temporary cache, uncertain notes, active context | Current task first |
| `99-Archive/` | Cold archive | Invalidated, expired, or superseded memory | Explicit recall only |

### Core Documents

| Document | Role |
| --- | --- |
| [PAMA Constitution v1.0](PAMA%20Constitution%20v1.0.md) | Supreme charter; defines user sovereignty and the AI's right to challenge false narratives |
| [PAMA V5.1 Stable](PAMA%20V5.1%20Stable.md) | Full personal memory architecture and layer model |
| [PAMA Deployment Spec v1.0](PAMA-Deployment-Spec-v1.0.md.md) | Physical Markdown/Obsidian implementation rules, metadata, confidence fields |
| [PAMA Prompt Intake Router](PAMA_Prompt_Intake_Router.md) | First-layer intent router for ambiguous or high-risk prompts |
| [PAMA Memory Write Router](PAMA_Memory_Write_Router.md) | Mandatory routing rules for user-requested permanent memory |
| [PAMA Root-Cause Fix Protocol](PAMA_Root_Cause_Fix_Protocol.md) | Mandatory protocol for fixing errors at their source layer |
| [PAMA Runtime Memory Policy](PAMA_Runtime_Memory_Policy.md) | Personal policy for keeping runtime memory temporary and low-authority |

Governance priority:

```text
Constitution > PAMA Stable Architecture > Deployment Spec > Prompt Intake Router / Memory Write Router / Root-Cause Fix Protocol / Runtime Memory Policy > Runtime behavior
```

### Memory Promotion Pipeline

```text
Conversation
Layer 0: transient context
        |
        v
08-Working-Memory
Layer 1: fast cache, low confidence, uncertain by default
        |
        v
07-Reviews
Evidence check, attention audit, decision feedback, confidence review
        |
        v
01-Reality / 03-Decisions / 05-Truth
Long-term memory, promoted only when evidence supports authority
```

### Agent Introspection Before Writing

Before writing or promoting memory, the AI agent should ask:

- Is this objective reality, a user interpretation, a temporary idea, or a durable truth?
- What evidence supports it?
- Is it still uncertain enough to store lower?
- Will it matter after the current conversation?
- Does it change future decisions or behavior?
- Is there an existing authoritative file that should be updated instead?
- Should this wait for a weekly or monthly review?

### Quick Start

1. Create the standard vault structure above.
2. Place the constitution, stable architecture, and deployment spec in `00-Core/`.
3. Configure your AI assistant's long-term memory path to the vault.
4. Use `08-Working-Memory/` for uncertain, active, or temporary memory.
5. Use `01-Reality/` for evidence-backed events and outcomes.
6. Use `07-Reviews/` as the promotion gate into `05-Truth/`.
7. Keep `05-Truth/` small, rare, and heavily verified.

### Ultimate Principle

PAMA should make memory more honest, not merely larger. A good personal AI memory system helps the user see reality more clearly while preserving the user's final authority.

<p align="center">
  <h1 align="center">ARMOR AI Workspace Architecture</h1>
  <p align="center"><strong>A long-term, stable, auditable memory architecture for AI agent workspaces</strong></p>
  <p align="center">V7.1 Stable &mdash; Deploy once, use continuously</p>
</p>

---

## Why This Exists

AI agents can generate endlessly. But without a structured memory system, their knowledge degrades: facts get overwritten, drafts become "truth," stale research drives decisions, and nobody can trace where an answer came from.

**ARMOR** solves this by giving your AI workspace a governed knowledge operating system &mdash; not just a vector store, but a layered, permission-controlled, lifecycle-managed memory architecture built on Obsidian Vault.

## Core Principles

| Principle | Meaning |
|---|---|
| **SSOT** (Single Source of Truth) | Every piece of knowledge has exactly one authoritative location. No parallel truths, no `final-final.md`. |
| **Capture ≠ Authority** | Agents can write freely into low-risk areas, but that doesn't make it true. Promotion requires review. |
| **Capability ≠ Permission** | The runtime *can* write files, but the protocol decides whether it *may*. |
| **Conservative Retrieval** | Default search excludes drafts, logs, raw research, archive, and unreviewed records. Only curated layers feed answers. |
| **Low-Maintenance** | Automatic lifecycle rules handle drafts, stale research, and inactive projects. Humans only review high-authority changes. |

## How It Works

### System Components

```text
┌─────────────────────────────────────────────────────┐
│                   Human Owner                        │
│              (final authority for                    │
│               high-risk changes)                     │
└──────────────────────┬──────────────────────────────┘
                       │ approves proposals
┌──────────────────────▼──────────────────────────────┐
│                    Hermes                            │
│         (primary agent / operating protocol)         │
│  retrieve · classify · summarize · propose · write   │
└──────────────────────┬──────────────────────────────┘
                       │ operates within
┌──────────────────────▼──────────────────────────────┐
│                   Claudian                           │
│           (Obsidian agent runtime)                   │
│    file I/O · search · skills · bash · MCP          │
└──────────────────────┬──────────────────────────────┘
                       │ reads/writes
┌──────────────────────▼──────────────────────────────┐
│                 Obsidian Vault                       │
│          (knowledge operating system)                │
│   storage · governance · graph · audit · review      │
└─────────────────────────────────────────────────────┘
```

### Five Memory Layers

| Layer | What It Stores | Example |
|---|---|---|
| **Working Memory** | Single-task context, discarded after use | Current conversation, retrieval results |
| **Facts** | Confirmed, current truth | Brand positioning, product pricing, customer profile |
| **Rules** | Reusable execution standards | SOPs, SEO rules, content standards |
| **Insights** | Validated experience | Cases, learnings, patterns, postmortems |
| **Research** | External, uncertain, time-sensitive knowledge | Market research, competitor analysis, SERP data |

Plus two supporting layers:

- **Records** &mdash; raw evidence (meeting notes, emails, transcripts). Evidence, not current truth.
- **Archive** &mdash; historical, deprecated, superseded material. Excluded from default retrieval.

### Two Operating Tracks

```text
┌─────────────────────────────┐    ┌─────────────────────────────┐
│       CAPTURE TRACK         │    │       AUTHORITY TRACK        │
│                             │    │                              │
│  90-Drafts                  │    │  00-Core                     │
│  91-Inbox                   │    │  01-Facts                    │
│  92-Logs                    │    │  02-Rules                    │
│  93-Proposals               │    │  03-Insights/Learnings       │
│  94-Review-Queues           │    │  04-Research/01-Reviewed     │
│  04-Research/00-Inbox       │    │                              │
│  05-Projects                │    │  Properties:                 │
│  06-Records                 │    │  • Small and stable          │
│                             │    │  • Source-backed             │
│  Properties:                │    │  • Reviewed where needed     │
│  • Fast write               │    │  • Default retrieval         │
│  • Low authority            │    │  • Protected by permissions  │
│  • Not current truth        │    │  • Modified slowly           │
│  • Auto-expires             │    │                              │
│  • May promote later        │    │                              │
└─────────────────────────────┘    └─────────────────────────────┘
         write freely                      change carefully
```

### Permission Model

| Class | Includes | Direct Write | Proposal Required |
|---|---|:---:|:---:|
| **A** | Core, Facts, Rules, Security Policy, Retrieval Rules | No | Yes + Human Approval |
| **B** | Customers, Decisions, Learnings, Research, Projects | Create/Append OK | For current-state changes |
| **C** | Drafts, Inbox, Logs, Proposals | Yes | No |
| **R** | Meetings, Emails, Transcripts, Raw Evidence | Append only | No |

## Vault Structure

```text
Vault/
│
├── 00-Core/                  # System constitution & principles
├── 01-Facts/                 # Confirmed truth (brand, products, customers)
├── 02-Rules/                 # Execution standards (SOPs, guidelines)
├── 03-Insights/              # Validated experience (cases, learnings)
├── 04-Research/              # External knowledge (market, competitor)
│   ├── 00-Inbox/             #   Raw, unreviewed research
│   └── 01-Reviewed/          #   Promoted, source-backed research
├── 05-Projects/              # Active project materials
├── 06-Records/               # Raw evidence (meetings, emails, transcripts)
│
├── 70-Schemas/               # Validation rules & templates
├── 80-Indexes/               # Cross-layer indexes
├── 81-Dashboards/            # Knowledge debt & evaluation dashboards
│
├── 90-Drafts/                # Unapproved working material
├── 91-Inbox/                 # Unclassified incoming content
├── 92-Logs/                  # Agent execution logs
├── 93-Proposals/             # Pending changes awaiting review
├── 94-Review-Queues/         # Scheduled review items
│
└── 99-Archive/               # Historical / deprecated material
```

The top-level structure is **frozen**. Domain-specific subfolders, templates, and content within layers are fully extensible.

## Lifecycle & Automation

Knowledge decays automatically:

| Content | Stale After | Archive After |
|---|---|---|
| Drafts | 30 days unused | 180 days unused |
| Inbox | 14 days unclassified | 30 days unresolved |
| Volatile Research | 30 days | 120 days total |
| Normal Research | 90 days | 180 days total |
| Inactive Projects | 30 days | 180 days |
| Logs | 30 days diagnostic value | 90 days |
| Pending Proposals | 30-day reminder | 90 days auto-expire |

Hermes handles classification, stale detection, conflict detection, duplicate detection, schema validation, and review queue preparation automatically. **Humans only review what affects authority.**

## Version History

| Version | Lines | Key Additions |
|---|---|---|
| [V4](ARMOR_AI_Workspace_Architecture_V4.md) | 1,024 | Foundation: SSOT, memory layers, basic vault structure |
| [V5](ARMOR_AI_Workspace_Architecture_V5.md) | 2,879 | Knowledge triage, promotion framework, conflict resolution, permission model |
| [V6](ARMOR_AI_Workspace_Architecture_V6.md) | 3,795 | Claudian runtime model, proposals layer, retrieval filter presets, naming conventions |
| [V7](ARMOR_AI_Workspace_Architecture_V7.md) | 5,404 | Runtime retrieval, context packing, schema validation, security & retention policy |
| [V7.1 Stable](ARMOR_AI_Workspace_Architecture_V7_1_Stable.md) | 4,129 | Architecture stability principle, Capture/Authority tracks, automatic lifecycle, low-maintenance ops |

## Documentation

| Document | Description |
|---|---|
| [V7.1 Stable (Full Spec)](ARMOR_AI_Workspace_Architecture_V7_1_Stable.md) | The complete architecture specification &mdash; 54 sections covering every aspect of the system |
| [Hermes Adaptation Guide](hermes_v71_complete_adaptation_guide.md) | Step-by-step guide for adapting Hermes to V7.1, including config, SOUL.md design, write/retrieval rules, and test cases |

## Quick Start

1. **Create the vault structure** using the frozen top-level layout above.
2. **Set up Core files**: `Core-Memory.md`, `Hermes-Operating-Protocol.md`, `Source-of-Truth-Map.md`, `Permission-Policy.md`, `Retrieval-Rules.md`.
3. **Configure Hermes** following the [Adaptation Guide](hermes_v71_complete_adaptation_guide.md) &mdash; point long-term memory to the Vault, set SQLite to runtime-only.
4. **Create templates** for Records, Proposals, Rules, and Research in `70-Schemas/Templates/`.
5. **Start capturing** &mdash; meeting notes go to Records, research goes to Research/Inbox, ideas go to Drafts.
6. **Review by exception** &mdash; only proposals affecting current truth, rules, or customer state need human approval.

## Design Philosophy

> The workspace does not optimize for remembering everything.
> It optimizes for preserving only governed, source-backed, reviewable, and useful memory.

- AI may **generate, classify, summarize, capture, archive, and propose**.
- AI may **not** silently convert uncertain information into facts, rules, or core memory.
- Truth is defined by SSOT files.
- Evidence is preserved in Records.
- Authority is controlled by the Permission Model.
- Retrieval is conservative by default.
- Unreviewed memory expires, degrades, or archives automatically.
- Only changes that affect current truth or future behavior require human approval.

## License

This project is released as an open architecture. Use it, adapt it, and build on it for your own AI workspace.

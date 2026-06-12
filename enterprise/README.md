# ARMOR Enterprise AI Workspace

> Enterprise-grade memory architecture for AI agents that need governed, auditable, source-backed business knowledge.

ARMOR Enterprise AI Workspace is the enterprise branch of AI Agent Memory Architecture. It is built for teams that use AI agents to operate on business-critical memory: brand facts, product specifications, customer profiles, SOPs, research, meeting records, decisions, and project knowledge.

ARMOR is not tied to a specific company or agent product. Any organization can adapt the structure, source-of-truth map, schemas, and review workflow to its own business domains.

**Current release:** V7.1 Stable + V7.1.5 Governance Patch

### Who It Is For

- Teams deploying AI agents inside real business workflows.
- Organizations that need auditable, source-backed AI memory.
- Multi-agent workspaces where knowledge consistency matters.
- Use cases where high-authority changes require human approval.
- Workspaces that need to separate raw evidence, working notes, reviewed research, and current truth.

### Who It Is Not For

- Simple chatbot memory with no governance requirement.
- Personal assistants where a lightweight single-user architecture is enough.
- Projects where every note can safely have the same authority.
- Systems that do not need provenance, retrieval controls, or review trails.

### Core Principles

| Principle | Meaning |
| --- | --- |
| **SSOT: Single Source of Truth** | Each business truth has one authoritative home. No parallel truths. |
| **Capture != Authority** | Fast capture is allowed, but captured text is not automatically true. |
| **Capability != Permission** | A runtime may be technically able to write, but the protocol decides whether it may write. |
| **Write != Truth** | Write permission does not grant truth authority. Confidence and source quality still matter. |
| **Conservative Retrieval** | Default retrieval excludes drafts, logs, raw research, records, proposals, and archives as current truth. |
| **Review by Exception** | Humans review only high-risk or authority-changing proposals. |
| **Low Maintenance** | Lifecycle rules age, expire, archive, and review content automatically where possible. |

### System Roles

```text
Human Owner / Reviewer
        |
        | approves high-risk proposals
        v
AI Agent
retrieve · classify · summarize · propose · write
        |
        | operates through
        v
Agent Runtime
file I/O · search · tools · MCP · indexes
        |
        | reads and writes
        v
Obsidian Vault / Markdown Knowledge OS
storage · governance · graph · audit · review
```

### Two Operating Tracks

ARMOR separates fast work from authoritative memory.

| Track | Typical Locations | Authority | Purpose |
| --- | --- | --- | --- |
| Capture Track | `90-Drafts/`, `91-Inbox/`, `92-Logs/`, `93-Proposals/`, `94-Review-Queues/`, `04-Research/00-Inbox/`, `05-Projects/`, `06-Records/` | Low or conditional | Capture quickly, preserve evidence, draft ideas, queue review |
| Authority Track | `00-Core/`, `01-Facts/`, `02-Rules/`, `03-Insights/`, `04-Research/01-Reviewed/` | High | Store governed truth, rules, reviewed research, validated learnings |

### Permission Model

| Class | Includes | Direct Write | Proposal Required |
| --- | --- | :---: | :---: |
| **A** | Core, Facts, Rules | No | Yes, with human approval |
| **B** | Insights, Reviewed Research, Projects | Create/append allowed | Required for state-changing or authority-changing edits |
| **C** | Drafts, Inbox, Logs, Review Queues | Yes | No |
| **R** | Records and evidence | Append only | No |

### V7.1.5 Governance Patch

The governance patch adds write-quality gates before information can become memory.

| Confidence Label | Source Pattern | Allowed Destination |
| --- | --- | --- |
| **High** | User-confirmed facts, official documents, verified specifications | Class A with controls, Class B/C/R |
| **Medium** | Multiple references, credible research summaries, partial evidence | Class B/C/R, not Class A directly |
| **Low** | AI inference, weak evidence, assumptions | Class C only |
| **No Memory** | Guesswork, irrelevant or temporary details | Do not store |

Fact creation gate:

```text
Before creating or updating 01-Facts/:
  1. Search existing authoritative memory.
  2. If an SSOT file exists, update through the proper policy.
  3. If there is a conflict, create a proposal.
  4. If the fact is new and high confidence, create through controlled write.
  5. If confidence is medium or low, store lower in research, insight, draft, or record layers.
```

### Vault Structure

```text
Vault/
├── 00-Core/                  # Constitution, operating protocol, SSOT map, policies
├── 01-Facts/                 # Confirmed current truth: brand, products, customers
├── 02-Rules/                 # SOPs, guidelines, reusable execution standards
├── 03-Insights/              # Validated cases, learnings, patterns, postmortems
├── 04-Research/              # External knowledge
│   ├── 00-Inbox/             # Raw, unreviewed research
│   └── 01-Reviewed/          # Reviewed, source-backed research
├── 05-Projects/              # Active project workspaces and closeouts
├── 06-Records/               # Raw evidence: meetings, emails, transcripts
├── 70-Schemas/               # Frontmatter schemas and templates
├── 80-Indexes/               # Cross-layer navigation
├── 81-Dashboards/            # Knowledge debt and memory health dashboards
├── 90-Drafts/                # Unapproved working material
├── 91-Inbox/                 # Unclassified incoming content
├── 92-Logs/                  # Agent execution logs
├── 93-Proposals/             # Pending changes awaiting review
├── 94-Review-Queues/         # Scheduled review items
└── 99-Archive/               # Deprecated, expired, superseded, or historical memory
```

The top-level structure is frozen. Add domain-specific folders inside the layers instead of changing the layer map.

### Agent Execution Layer

ARMOR can be operated by any trusted agent runtime with file read/search/write/patch capability, including Hermes, Claude Code, Codex, Opencode, Cline, OpenHands, and custom agents. The runtime is an executor, not an authority layer.

Use the runtime to read, search, draft, append records, create proposals, update allowed project files, and write execution logs. Do not use the runtime to bypass Class A protections, silently update Facts or Rules, treat Records as current Facts, or let runtime memory become durable business memory.

Recommended relationship:

```text
ARMOR defines permission.
A trusted runtime executes allowed Vault operations.
Human review approves authority-changing proposals.
```

See [Agent Runtime Adaptation Guide](agent_runtime_adaptation_guide.md) for the ARMOR-native handoff locations, permission matrix, executor protocol, and execution log template.

### Lifecycle Rules

| Content | Stale After | Archive or Expire After |
| --- | --- | --- |
| Drafts | 30 days unused | 180 days unused |
| Inbox | 14 days unclassified | 30 days unresolved |
| Volatile research | 30 days | 120 days total |
| Normal research | 90 days | 180 days total |
| Inactive projects | 30 days | 180 days |
| Logs | 30 days diagnostic value | 90 days |
| Pending proposals | 30-day reminder | 90 days auto-expire |

### Quick Start

1. Create the frozen vault structure above.
2. Set up core files such as `Core-Memory.md`, `Agent-Operating-Protocol.md`, `Source-of-Truth-Map.md`, `Permission-Policy.md`, `Retrieval-Rules.md`, `Prompt-Intake-Router.md`, `Memory-Write-Router.md`, `Root-Cause-Fix-Protocol.md`, `Runtime-Memory-Policy.md`, `Lifecycle-Policy.md`, and `Governance-Patch-V715.md`.
3. Configure the AI agent's long-term memory path to this vault.
4. Keep SQLite, embeddings, and runtime indexes as runtime-only infrastructure. They must not become the durable source of business truth.
5. Create templates for records, proposals, rules, research, and reviewed insights under `70-Schemas/`.
6. Let agents capture into low-authority layers and require proposals for authority-changing edits.

### Documents

| Document | Description |
| --- | --- |
| [V7.1 Stable](V7_1_Stable.md) | Full enterprise architecture specification |
| [V7.1.5 Governance Patch](V7_1_5_Governance_Patch.md) | Source confidence, write-quality gates, fact creation rules |
| [Prompt Intake Router](Prompt_Intake_Router.md) | First-layer intent router for ambiguous or high-risk prompts |
| [Memory Write Router](Memory_Write_Router.md) | Mandatory routing rules for user-requested permanent memory |
| [Root-Cause Fix Protocol](Root_Cause_Fix_Protocol.md) | Mandatory protocol for fixing errors at their source layer |
| [Runtime Memory Policy](Runtime_Memory_Policy.md) | Enterprise policy for keeping runtime memory low-authority and temporary |
| [Agent Runtime Adaptation Guide](agent_runtime_adaptation_guide.md) | Practical guide for using any trusted agent runtime as an ARMOR executor |

### Ultimate Principle

ARMOR does not optimize for remembering everything. It optimizes for preserving governed, source-backed, reviewable, and operationally useful memory.

# ARMOR AI Workspace Architecture V7.1 Stable

## Version

Version: V7.1 Stable  
System: ARMOR AI Workspace  
Primary Agent / Protocol: Hermes  
Knowledge Runtime: Claudian  
Knowledge System: Obsidian Vault  
Purpose: Long-term, stable, auditable, controllable AI workspace memory architecture  
Status: Stable architecture for one-time deployment and continuous long-term use  
Primary Upgrade from V7: Architecture stability principle, low-maintenance operations, Capture Track / Authority Track, conservative retrieval, automatic lifecycle rules, review-by-exception

---

# Table of Contents

1. Vision
2. Architecture Stability Principle
3. First Principle: SSOT
4. System Roles
5. Claudian Runtime Model
6. Hermes Operating Protocol
7. Memory Model
8. Capture Track and Authority Track
9. Vault Structure
10. Core Layer
11. Source of Truth System
12. Facts Layer
13. Rules Layer
14. Insights Layer
15. Research Layer
16. Projects Layer
17. Records Layer
18. Indexes and Dashboards Layer
19. Temporary Layers
20. Proposals Layer
21. Review Queues Layer
22. Archive Layer
23. Knowledge Triage Rules
24. Knowledge Promotion Framework
25. Conflict Resolution Policy
26. Permission Model
27. Write Speed Policy
28. Memory Write Pipeline
29. Agent Write Rules
30. Retrieval Runtime Architecture
31. Retrieval Ranking and Scoring
32. Context Packing Policy
33. Retrieval Filter Presets
34. Knowledge Graph Metadata
35. Schema Validation Layer
36. Changelog Requirement
37. Naming Convention
38. File Lifecycle
39. Automatic Lifecycle Rules
40. Review and Audit
41. Low-Maintenance Operations
42. Knowledge Debt Dashboard
43. Memory Evaluation Metrics
44. Security, Privacy, and Retention Policy
45. Backup and Recovery Policy
46. Standard Templates
47. Claudian Skills and Workflows
48. Automation and Enforcement
49. Human Review UX
50. Failure Modes and Recovery
51. Operating Cadence
52. Migration / Deployment Plan
53. Success Criteria
54. Ultimate Principle

---

# 1. Vision

The goal is not to build an AI that remembers everything.

The goal is to build a long-term AI workspace that remains stable, auditable, controllable, useful, and low-maintenance over time.

The workspace must always know:

- where current truth lives
- where rules live
- where raw evidence lives
- where research lives
- whether research is stale
- which files are authoritative
- which files are only drafts
- which files are only records
- which content can be retrieved by default
- which content must be excluded from default retrieval
- which changes require human approval
- which changes can be made automatically
- how knowledge is promoted
- how conflicts are resolved
- how memory decays, archives, or expires
- why a memory was used in an answer
- whether the memory system is improving or degrading

AI can generate endlessly.

The knowledge base must converge.

V7.1 Stable is designed around five principles:

```text
One-time deployment
Stable architecture
Low-maintenance operations
Conservative retrieval
Human approval only for high-authority changes
```

---

# 2. Architecture Stability Principle

This architecture is designed to be deployed once and used continuously without structural redesign.

Top-level layers, memory roles, permission classes, retrieval defaults, and lifecycle rules are considered stable architecture. They should not be changed unless the fundamental purpose of the workspace changes.

Future changes should be limited to:

- adding files within existing layers
- adding domain-specific subfolders
- updating templates
- improving automation
- refining schemas
- tuning review cadence
- improving dashboards
- improving retrieval implementation

Future changes should not require:

- changing top-level folders
- merging memory layers
- redefining Records as Facts
- allowing Drafts as current truth
- moving Archive back into default retrieval
- letting agent output silently become authoritative

The system must prefer progressive usage over structural migration.

## 2.1 Frozen Architecture Boundary

Frozen:

```text
00-Core/
01-Facts/
02-Rules/
03-Insights/
04-Research/
05-Projects/
06-Records/
70-Schemas/
80-Indexes/
81-Dashboards/
90-Drafts/
91-Inbox/
92-Logs/
93-Proposals/
94-Review-Queues/
99-Archive/
```

Also frozen:

- memory layer definitions
- SSOT principle
- Records vs Facts separation
- permission classes
- default retrieval exclusions
- Capture Track / Authority Track
- automatic lifecycle rules
- proposal requirement for high-authority changes

Expandable:

- domain-specific folders
- product folders
- customer folders
- project folders
- rule categories
- research categories
- templates
- schema details
- automation scripts
- dashboards

Principle:

```text
Architecture layer is stable.
Domain layer is extensible.
Content layer evolves continuously.
```

---

# 3. First Principle: SSOT

SSOT means Single Source of Truth.

Every formal piece of knowledge must have exactly one authoritative location.

Allowed:

- references
- backlinks
- index views
- dashboards
- Dataview queries
- summaries that point to authority
- proposals
- changelogs
- timelines
- Git history
- append-only source records
- superseded records

Forbidden:

- duplicated authority
- parallel truths
- multiple current versions
- unmarked outdated facts
- final-final files
- using meeting notes as customer current state
- using research as fact
- using cases as rules
- using archive as current truth
- using drafts as approved memory

Wrong:

```text
Product-A-v1.md
Product-A-v2.md
Product-A-final.md
Product-A-final-final.md
```

Correct:

```text
Product-A.md
```

Historical changes must be preserved through:

- changelog
- timeline
- Git history
- source records
- append-only history
- proposal records
- superseded markers

Do not create multiple authority files for convenience.

---

# 4. System Roles

## 4.1 Obsidian

Role: Knowledge System

Obsidian is the long-term knowledge operating system.

Responsibilities:

- durable knowledge storage
- knowledge governance
- relationship graph
- audit trail
- human review interface
- evidence storage
- authoritative memory storage
- lifecycle management

Principle:

```text
Vault is the only long-term memory.
```

Obsidian is not just a notes app.

It is the AI workspace knowledge operating system.

## 4.2 Claudian

Role: Obsidian Agent Runtime

Claudian is the runtime that allows AI agents to operate inside Obsidian.

Capabilities may include:

- file read
- file write
- file edit
- file search
- chat sidebar
- inline edit
- slash commands
- skills
- `@mention` Vault files
- `@mention` subagents
- `@mention` MCP servers
- plan mode
- instruction mode
- bash
- workflows
- external file access

Principle:

```text
Capability does not equal permission.
```

Claudian may technically allow writing files.

Hermes may still be forbidden from modifying certain files by the Permission Model.

Claudian is not:

- long-term memory
- source of truth
- final reviewer
- governance layer
- automatic SSOT enforcement

Claudian provides capability.

Hermes protocol and Vault governance define permission.

## 4.3 Hermes

Role: Primary AI Workspace Agent / Operating Protocol

Hermes can:

- retrieve
- analyze
- summarize
- draft
- classify
- propose
- write low-risk notes
- append records
- generate review candidates
- detect conflicts
- create proposals
- assist project closeout
- assist memory evaluation
- assist schema validation

Hermes must:

- respect SSOT
- classify knowledge before writing
- check Source of Truth System before formal updates
- respect Permission Model
- create proposals for Class A assets
- avoid silent promotion
- avoid treating Records as Facts
- avoid treating Research as Facts
- avoid treating Cases as Rules
- avoid default retrieval from Drafts, Logs, Inbox, Raw Research, or Archive
- cite sources when required
- mark stale or uncertain memory
- reduce authority when unsure

Principle:

```text
Hermes may capture, classify, summarize, archive, and propose.
Hermes may not silently convert uncertain information into truth.
```

## 4.4 Human Owner / Reviewer

Role: Final Authority for high-authority changes

The Human Owner approves changes that affect:

- current truth
- system behavior
- customer current state
- brand facts
- product facts
- approved rules
- security posture
- permission policy
- conflict resolution

Principle:

```text
Human approval defines truth for high-risk knowledge.
```

Agent output is not truth until reviewed or explicitly confirmed.

## 4.5 Knowledge Steward

Role: Optional Knowledge Operations Owner

In V7.1 Stable, this role should be minimized.

Responsibilities, if assigned:

- monitor knowledge debt
- review stale queues
- process proposals
- clean old drafts
- inspect schema failures
- check archive leakage
- assist project closeout

If no dedicated Knowledge Steward exists, Hermes should automate most operational preparation, and the Human Owner should only review high-authority items.

---

# 5. Claudian Runtime Model

Claudian is the runtime layer.

Hermes is the protocol layer.

The Vault is the memory layer.

Human review is the authority layer.

```text
Runtime capability
↓
Hermes protocol
↓
Permission model
↓
Vault write path
↓
Human approval where required
```

## 5.1 Runtime Boundary

Claudian does not automatically:

- determine truth
- maintain SSOT
- solve conflicts
- approve facts
- distinguish raw evidence from current truth
- determine research freshness
- enforce retention policy

These must be defined by architecture and enforced by workflow, scripts, schemas, or review.

## 5.2 Plan Mode Policy

Hermes must use Plan Mode or equivalent proposal workflow when working with:

- Core Memory
- Source of Truth System
- Permission Policy
- Retrieval Rules
- Context Packing Policy
- Security Policy
- Brand Facts
- Product Facts
- Customer current profile
- Approved Rules
- Schema updates
- Reviewed Research promotion
- Learning to Rule promotion
- Archive restoration

Plan workflow:

```text
Explore
↓
Identify target files
↓
Check Source of Truth System
↓
Check Permission Class
↓
Generate plan
↓
Generate proposal
↓
Human approval
↓
Apply or reject
↓
Update changelog
↓
Update indexes if needed
```

## 5.3 `@mention` Policy

For formal memory changes, Hermes should explicitly reference relevant authority files.

Class A changes should reference:

```text
@Core-Memory.md
@Source-of-Truth-Map.md
@Permission-Policy.md
@Relevant-SSOT-File.md
```

Customer current state changes should reference:

```text
@Customer/profile.md
@Relevant record
@Relevant timeline entry
@Proposal file
```

Rule changes should reference:

```text
@Relevant rule
@Supporting facts
@Supporting cases or learnings
@Proposal file
```

Research promotion should reference:

```text
@Raw research file
@Reviewed source summary
@Relevant facts or rules
@Proposal file
```

---

# 6. Hermes Operating Protocol

Hermes follows the same sequence for every task.

## 6.1 Start of Task

Hermes determines:

```text
Is this execution only?
Is this retrieval?
Is this knowledge creation?
Is this knowledge update?
Is this high-risk modification?
Is this research?
Is this project work?
Is this source record ingestion?
Is this audit or evaluation?
```

If the task is temporary execution, no long-term memory is written.

If long-term memory is involved, Hermes enters the Memory Write Pipeline.

## 6.2 Before Retrieval

Hermes determines which layers are relevant:

```text
Core?
Facts?
Rules?
Insights?
Reviewed Research?
Active Project?
Records / evidence?
Archive / history?
Logs / debug?
```

Default retrieval excludes:

- Archive
- Logs
- Drafts
- Inbox
- Raw Research
- Proposals
- Review Queues
- Deprecated files
- Superseded files
- Records unless evidence is needed

## 6.3 Before Writing

Hermes must determine:

```text
What type of knowledge is this?
Where is the SSOT?
Is this raw evidence or interpreted knowledge?
What is the permission class?
Does this need source?
Does this need review_date?
Does this need expires_at?
Does this need changelog?
Can Hermes write directly?
Should Hermes create a proposal?
```

## 6.4 After Writing

Hermes must add appropriate metadata:

- type
- memory_layer
- status
- authority
- source
- updated
- write_policy
- sensitivity where needed
- review_date or expires_at where needed
- related links where useful
- changelog where required

Hermes must avoid creating duplicate authority files.

Unclear content goes to Inbox.

High-risk updates become proposals.

## 6.5 Before Answering with Memory

Hermes must check:

```text
Did I use SSOT where available?
Did I avoid Drafts, Logs, Raw Research, and Archive as current truth?
Did I distinguish fact from research?
Did I distinguish record from current state?
Is any memory stale?
Do I need to cite memory sources?
```

For high-risk answers, Hermes should report:

- authority files used
- evidence records used
- whether anything is stale or uncertain
- whether human confirmation is needed

---

# 7. Memory Model

The system uses five memory layers.

## 7.1 Layer 1 — Working Memory

Lifecycle: single task

Sources:

- current user request
- current conversation
- current retrieval results
- current project context

Properties:

- temporary
- not automatically stored
- not authoritative
- destroyed or ignored after task unless explicitly written

Forbidden:

- treating temporary reasoning as long-term fact
- silently writing to Core
- silently updating authoritative memory

## 7.2 Layer 2A — Facts Memory

Stores confirmed truth.

Examples:

- brand facts
- product facts
- customer current state
- confirmed decisions
- current parameters
- current business information

Facts are what is true.

Facts are not:

- raw records
- drafts
- research
- cases
- rules

Facts are divided into:

### Current Facts

Current, active truth.

Examples:

- current product pricing
- current brand positioning
- current customer objective
- current service scope

Current Facts may be updated, but history must be preserved.

### Historical Facts

Confirmed past truth.

Examples:

- customer objective in 2025
- old pricing
- past decision
- completed phase result

Historical Facts are append-only by default.

## 7.3 Layer 2B — Rules Memory

Stores reusable execution standards.

Examples:

- SOPs
- SEO rules
- Social rules
- Agent rules
- content standards
- automation standards

Rules are how things should be done.

Rules are not facts.

Rules are not cases.

Rules require review.

## 7.4 Layer 2C — Insights Memory

Stores validated experience.

Includes:

- cases
- learnings
- patterns
- postmortems

Definitions:

```text
Case = what happened
Learning = what was learned and when it applies
Pattern = repeated observation
Postmortem = structured analysis of important success or failure
```

A single event is not a rule.

A single success is not a learning.

Repeated evidence or human confirmation is required for promotion.

## 7.5 Layer 3 — Research Memory

Stores external, uncertain, or time-sensitive knowledge.

Examples:

- market research
- competitor research
- platform rule observations
- SERP analysis
- industry trends
- technical research

Research must have:

- source
- confidence
- review_date or expires_at

Research can support judgment.

Research does not define current truth.

## 7.6 Layer 4 — Records Memory

Stores raw evidence.

Examples:

- meeting notes
- transcripts
- customer emails
- raw feedback
- imported documents
- screenshots
- attachments
- signed approvals
- raw interview notes

Records are evidence.

Records are not current truth by default.

Records can support Facts, Decisions, Cases, Learnings, or Proposals.

## 7.7 Layer 5 — Archive Memory

Stores historical, inactive, deprecated, or superseded material.

Archive is not current truth.

Archive is excluded from default retrieval.

Archive can be used only for:

- history
- audit
- recovery
- comparison
- conflict investigation

---

# 8. Capture Track and Authority Track

V7.1 Stable uses a two-track operating model.

## 8.1 Capture Track

Purpose: capture information freely without polluting truth.

Includes:

```text
90-Drafts/
91-Inbox/
92-Logs/
04-Research/00-Inbox/
05-Projects/
06-Records/
93-Proposals/
94-Review-Queues/
```

Properties:

- Hermes can write freely or append
- low authority
- not current truth
- not included in default authoritative retrieval
- may expire, degrade, or archive automatically
- may be promoted later

Principle:

```text
Capture does not equal authority.
```

## 8.2 Authority Track

Purpose: preserve stable, high-quality memory.

Includes:

```text
00-Core/
01-Facts/
02-Rules/
03-Insights/Learnings/
04-Research/01-Reviewed/
```

Properties:

- small and stable
- source-backed
- reviewed where needed
- participates in default retrieval
- modified slowly
- protected by permission model

Principle:

```text
High-authority memory must be small, stable, source-backed, and rarely changed.
```

## 8.3 Review by Exception

Most captured information remains low-authority unless explicitly promoted.

Human review is required only when a change affects:

- current truth
- approved rules
- system behavior
- customer current state
- product facts
- brand facts
- security posture
- permission model
- retrieval behavior
- conflict resolution

This keeps the system low-maintenance.

---

# 9. Vault Structure

The top-level structure is frozen.

```text
Vault/

00-Core/
01-Facts/
02-Rules/
03-Insights/
04-Research/
05-Projects/
06-Records/

70-Schemas/
80-Indexes/
81-Dashboards/

90-Drafts/
91-Inbox/
92-Logs/
93-Proposals/
94-Review-Queues/

99-Archive/
```

Layer meanings:

```text
00-06: formal memory, work, knowledge, and evidence
70: schema and validation definitions
80-81: indexes and dashboards
90-94: temporary, operational, and review layers
99: historical archive
```

Key rule:

```text
Meeting notes, emails, transcripts, and raw feedback belong in 06-Records, not 01-Facts.
```

---

# 10. Core Layer

Location:

```text
00-Core/
```

Role: system constitution

Contains:

- system principles
- SSOT principle
- Hermes behavior rules
- permission model
- retrieval rules
- context packing rules
- knowledge triage rules
- conflict resolution policy
- security and retention policy
- lifecycle policy

Core should be small, stable, and rarely changed.

Core should not contain:

- product details
- brand details
- customer facts
- research conclusions
- project notes
- raw records

## 10.1 Recommended Core Files

```text
00-Core/
  Core-Memory.md
  Hermes-Operating-Protocol.md
  Source-of-Truth-Map.md
  Permission-Policy.md
  Retrieval-Rules.md
  Context-Packing-Policy.md
  Knowledge-Triage-Rules.md
  Conflict-Resolution-Policy.md
  Security-and-Retention-Policy.md
  Lifecycle-Policy.md
```

Optional later files:

```text
  Claudian-Runtime-Policy.md
  Schema-Validation-Policy.md
  Backup-and-Recovery-Policy.md
  Automation-Enforcement-Policy.md
```

Do not split Core excessively unless operational complexity requires it.

---

# 11. Source of Truth System

The Source of Truth System defines where each type of knowledge lives.

It includes:

```text
1. Human-readable Source-of-Truth-Map.md
2. Optional machine-readable registry
3. Indexes generated from metadata
4. Duplicate and conflict queues
```

## 11.1 Source of Truth Map

Location:

```text
00-Core/Source-of-Truth-Map.md
```

Example:

| Knowledge | SSOT Location | Editable By | Review Required |
|---|---|---|---|
| Core principles | `00-Core/Core-Memory.md` | Proposal only | Yes |
| Hermes behavior rules | `00-Core/Hermes-Operating-Protocol.md` | Proposal only | Yes |
| Retrieval rules | `00-Core/Retrieval-Rules.md` | Proposal only | Yes |
| Brand positioning | `01-Facts/Brand/Positioning.md` | Proposal only | Yes |
| Product facts | `01-Facts/Products/` | Proposal only | Yes |
| Customer current profile | `01-Facts/Customers/{customer}/profile.md` | Proposal only | Yes |
| Customer timeline | `01-Facts/Customers/{customer}/timeline/` | Hermes append | Review by exception |
| Decisions | `01-Facts/Decisions/` | Proposal or confirmed write | Yes |
| Approved rules | `02-Rules/` | Proposal only | Yes |
| Cases | `03-Insights/Cases/` | Hermes create | Review by exception |
| Learnings | `03-Insights/Learnings/` | Proposal for approval | Yes |
| Research inbox | `04-Research/00-Inbox/` | Hermes write | No |
| Reviewed research | `04-Research/01-Reviewed/` | Proposal only | Yes |
| Projects | `05-Projects/` | Hermes write | Closeout by lifecycle |
| Records | `06-Records/` | Hermes append | No by default |
| Drafts | `90-Drafts/` | Hermes write | No |
| Inbox | `91-Inbox/` | Hermes write | No |
| Logs | `92-Logs/` | Hermes write | No |
| Proposals | `93-Proposals/` | Hermes write | Human decision |
| Review queues | `94-Review-Queues/` | Hermes write | Review by exception |
| Archive | `99-Archive/` | Archive workflow | No default retrieval |

## 11.2 Source of Truth Registry

Optional machine-readable registry:

```text
00-Core/Source-of-Truth-Registry/
  Brand.yml
  Products.yml
  Customers.yml
  Rules.yml
  Research.yml
  Records.yml
  Projects.yml
```

Example:

```yaml
knowledge_domain: products
ssot_root: 01-Facts/Products/
file_pattern: "{Product-Name}.md"
permission_class: A
write_policy: proposal_only
required_schema: product.schema.yml
required_review: true
default_retrieval: true
archive_retrieval: false
```

If the Map and Registry conflict, create a conflict proposal.

If no SSOT is defined, write to Inbox and create a triage note.

---

# 12. Facts Layer

Location:

```text
01-Facts/
```

Purpose: confirmed truth

Recommended structure:

```text
01-Facts/
  Brand/
  Products/
  Customers/
  Decisions/
```

Facts are what is true.

Facts are not raw records, research, rules, or drafts.

## 12.1 Brand

Location:

```text
01-Facts/Brand/
```

Stores:

- brand positioning
- brand values
- tone of voice
- audience definition
- messaging
- visual guidelines
- prohibited claims

Recommended files:

```text
Brand/
  Positioning.md
  Tone-of-Voice.md
  Audience.md
  Messaging.md
  Visual-Guidelines.md
```

Brand facts are Class A.

Hermes may only propose changes.

## 12.2 Products

Location:

```text
01-Facts/Products/
```

One product, one authority file.

Example:

```text
Products/
  Armor-SEO.md
  Armor-AI.md
  Hermes-Agent.md
```

Stores:

- positioning
- features
- current pricing
- current packages
- target customers
- constraints
- claims
- related rules
- related cases

Product facts are Class A.

No `v2`, `new`, `final`, or duplicate authority files.

## 12.3 Customers

Location:

```text
01-Facts/Customers/
```

Recommended structure:

```text
Customers/
  Acme/
    profile.md
    timeline/
      2026.md
    assets/
```

`profile.md` stores current customer state:

- industry
- business model
- current goals
- current pain points
- current cooperation status
- current owner
- current risk
- current opportunity
- current service scope

Customer profile is Class B with proposal requirement for current-state changes.

Meeting notes and emails do not live here.

They live in:

```text
06-Records/Customers/{customer}/
```

## 12.4 Timeline

Location:

```text
01-Facts/Customers/{customer}/timeline/
```

Purpose: append-only history

Records:

- decisions
- milestones
- scope changes
- budget changes
- status changes
- important risks
- important conclusions

Timeline append can be fast, but should cite source.

Timeline is historical.

It does not override current profile unless profile is updated through proper workflow.

## 12.5 Decisions

Location:

```text
01-Facts/Decisions/
```

Purpose: confirmed decisions

Naming:

```text
YYYY-MM-DD-Decision-Name.md
```

Required content:

- date
- context
- options considered
- decision
- decided by
- reason
- impacted files
- source
- follow-up

Decision is not the same as meeting note.

A meeting note may support a decision.

---

# 13. Rules Layer

Location:

```text
02-Rules/
```

Purpose: reusable execution standards

Recommended structure:

```text
02-Rules/
  SEO/
  Social/
  SOP/
  Agents/
  Content/
  Sales/
  Automation/
```

Rules describe how work should be done.

Rules are Class A or high-control Class B.

Hermes may propose changes but should not silently modify approved rules.

## 13.1 Rule Requirements

Each approved rule should include:

- purpose
- scope
- trigger/input condition
- steps
- output standard
- quality standard
- exceptions
- prohibited actions
- owner
- source
- review_date
- changelog

## 13.2 Rule Qualification Checklist

A rule must be:

```text
repeatable
clear in trigger
clear in output
clear in exceptions
supported by source, decision, case, or learning
owned
reviewable
approved
```

If not, it remains Draft, Case, Learning, or Proposal.

---

# 14. Insights Layer

Location:

```text
03-Insights/
```

Purpose: experience memory

Recommended structure:

```text
03-Insights/
  Cases/
  Learnings/
  Patterns/
  Postmortems/
```

Insights are what the system has learned from experience.

Insights are not current facts.

Insights are not rules unless promoted.

## 14.1 Cases

Cases record what happened.

A case should include:

- background
- participants
- action taken
- result
- evidence
- related project
- related customer

Cases may be created by Hermes.

Cases do not automatically become Learnings.

## 14.2 Learnings

Learnings explain what seems to work or fail, and under what conditions.

A learning should include:

- observation
- evidence
- conditions
- limitations
- applicability
- confidence
- related cases
- review_date

Learning approval requires review.

## 14.3 Patterns

Patterns are repeated observations across cases, projects, or customers.

Patterns may support Learnings.

## 14.4 Postmortems

Postmortems analyze important failures, incidents, or major successes.

Postmortems may produce:

- cases
- learnings
- rule proposals
- process changes

---

# 15. Research Layer

Location:

```text
04-Research/
```

Purpose: external or uncertain knowledge

Structure:

```text
04-Research/
  00-Inbox/
  01-Reviewed/
  80-Reference/
  90-Review-Queue/
  99-Archive/
```

## 15.1 Research Inbox

Location:

```text
04-Research/00-Inbox/
```

Hermes may write freely.

Properties:

- low authority
- unreviewed
- requires source
- not default retrieval
- expires or archives automatically

## 15.2 Reviewed Research

Location:

```text
04-Research/01-Reviewed/
```

Properties:

- reviewed
- source-backed
- has review_date
- has expires_at or next_review
- can support answers
- still not equal to fact

## 15.3 Reference

Location:

```text
04-Research/80-Reference/
```

Stores relatively stable external background:

- terminology
- long-term frameworks
- evergreen references
- technical background

Reference should still have review_date.

## 15.4 Research Review Queue

Location:

```text
04-Research/90-Review-Queue/
```

Used for research that may be stale.

## 15.5 Research Archive

Location:

```text
04-Research/99-Archive/
```

Stores:

- outdated research
- replaced competitor notes
- old SERP analysis
- invalidated market observations

Archive is excluded from default retrieval.

## 15.6 Research Freshness Classes

Research should use freshness classes instead of one universal timeline.

```yaml
freshness_class:
  volatile_30d: pricing, platform rules, competitor offers, SERP data
  normal_90d: market research, tactical analysis, tool comparisons
  stable_180d: frameworks, strategy references, durable industry analysis
  evergreen_365d: terminology, foundational concepts, historical context
```

---

# 16. Projects Layer

Location:

```text
05-Projects/
```

Purpose: active workspaces

Projects can contain:

- briefs
- plans
- notes
- research
- drafts
- deliverables
- working decisions
- project-specific context

Recommended structure:

```text
05-Projects/
  Project-A/
    brief.md
    plan.md
    research.md
    notes/
    drafts/
    deliverables/
    decisions.md
    closeout.md
```

Projects are not permanent knowledge by default.

Project closeout extracts reusable knowledge into proper layers.

## 16.1 Project Closeout

When a project ends:

```text
Project ends
↓
Closeout review
↓
Extract knowledge
↓
Promote to Facts / Rules / Cases / Learnings / Records / Archive
↓
Archive project
```

Extract:

- new facts → Facts proposal
- customer changes → Customer profile proposal or timeline append
- raw materials → Records
- events → Cases
- reusable lessons → Learnings
- reusable process → Rule proposal
- inactive project files → Archive

---

# 17. Records Layer

Location:

```text
06-Records/
```

Purpose: raw evidence

Structure:

```text
06-Records/
  Customers/
    Acme/
      Meetings/
      Emails/
      Calls/
      Feedback/
      Attachments/
  Internal/
    Meetings/
    Decisions-Raw/
    Strategy-Notes/
  Sources/
    Web/
    PDFs/
    Screenshots/
    Imports/
```

Records are append-only by default.

Records require sensitivity metadata.

Records do not equal current truth.

Records can support:

- Facts
- Decisions
- Cases
- Learnings
- Proposals
- Conflict resolution

## 17.1 Records Principles

Forbidden:

- treating a single quote as customer profile
- treating meeting discussion as decision
- treating email claim as product fact
- rewriting records silently
- using Records as default current truth

Allowed:

- append record
- add correction note
- cite record as evidence
- create promotion proposal
- link record to timeline

## 17.2 Record Promotion

Possible paths:

```text
Meeting note → Decision proposal
Meeting note → Customer profile proposal
Email → Timeline append
Feedback → Case
Repeated feedback → Learning
Transcript → Project note
Raw source → Research
Signed approval → Decision / Fact evidence
```

Promotion requires triage.

---

# 18. Indexes and Dashboards Layer

## 18.1 Indexes

Location:

```text
80-Indexes/
```

Purpose: navigation and aggregation

Recommended files:

```text
80-Indexes/
  Products.md
  Customers.md
  Active-Projects.md
  Rules.md
  Learnings.md
  Records.md
  Research.md
  Review-Queue.md
  Duplicate-Candidates.md
  Deprecated-Knowledge.md
```

Indexes point to truth.

Indexes do not become truth.

## 18.2 Dashboards

Location:

```text
81-Dashboards/
```

Purpose: operational visibility

Recommended dashboards:

```text
81-Dashboards/
  Knowledge-Debt-Dashboard.md
  Memory-Evaluation-Dashboard.md
  Proposal-Dashboard.md
  Research-Freshness-Dashboard.md
  Project-Closeout-Dashboard.md
  Security-Retention-Dashboard.md
```

Dashboards should be generated where possible.

Dashboards are not authority.

---

# 19. Temporary Layers

## 19.1 Drafts

Location:

```text
90-Drafts/
```

Purpose: working drafts

Properties:

- open write
- no authority
- excluded from default retrieval
- can be deleted or archived
- can be promoted only through triage

## 19.2 Inbox

Location:

```text
91-Inbox/
```

Purpose: unclassified content

Properties:

- open write
- no authority
- temporary
- automatically triaged or archived

Inbox outcomes:

- delete
- archive
- draft
- research
- record
- project
- proposal
- formal knowledge after review

## 19.3 Logs

Location:

```text
92-Logs/
```

Purpose: operational trace

Stores:

- task logs
- errors
- automation failures
- execution summaries
- debug traces

Logs are excluded from default retrieval.

Logs can support postmortems or automation learnings.

---

# 20. Proposals Layer

Location:

```text
93-Proposals/
```

Purpose: reviewable change requests

Structure:

```text
93-Proposals/
  Core/
  Facts/
  Rules/
  Customers/
  Research/
  Records/
  Conflicts/
  Promotions/
  Archive/
  Schemas/
  Security/
```

Proposals are not truth.

Proposals are pending suggestions.

## 20.1 When to Create Proposal

Required for:

- Core changes
- Source of Truth System changes
- Permission Policy changes
- Retrieval Rules changes
- Context Packing Policy changes
- Security Policy changes
- Schema changes
- Brand facts
- Product facts
- Customer current profile
- Approved Rules
- Learning to Rule promotion
- Research to Reviewed Research promotion
- Conflict resolution
- duplicate authority merge
- Archive restoration
- marking formal knowledge deprecated or superseded

## 20.2 Proposal Lifecycle

```text
Drafted
↓
Pending Review
↓
Approved / Rejected / Needs Revision / Expired
↓
Applied if approved
↓
Changelog updated
↓
Indexes updated if needed
↓
Proposal archived
```

## 20.3 Proposal Requirements

Each proposal should include:

- target_file
- proposal_type
- proposed_change
- reason
- source_evidence
- risk
- affected_files
- suggested_changelog_entry
- rollback_plan for high-risk updates
- reviewer
- decision

---

# 21. Review Queues Layer

Location:

```text
94-Review-Queues/
```

Purpose: operational review lists

Recommended files:

```text
94-Review-Queues/
  Review-Queue.md
  Proposal-Queue.md
  Conflict-Queue.md
  Records-Triage.md
  Expiring-Research.md
  Duplicate-Candidates.md
  Orphan-Notes.md
  Schema-Failures.md
  Project-Closeout-Queue.md
  Security-Review.md
```

V7.1 Stable uses review by exception.

Queues should not become large manual obligations.

Hermes should generate queue entries, summaries, and recommended actions.

Human review focuses only on high-authority impact.

---

# 22. Archive Layer

Location:

```text
99-Archive/
```

Purpose: historical storage

Stores:

- completed projects
- outdated research
- deprecated rules
- superseded files
- closed customer records
- rejected or expired proposals
- old drafts
- old logs
- invalidated knowledge

Archive is excluded from default retrieval.

Archive may be used for:

- historical tracing
- audit
- recovery
- conflict analysis

If archived content becomes useful again, it must be reviewed before restoration.

---

# 23. Knowledge Triage Rules

All write operations must classify knowledge first.

## 23.1 Classification

```text
Current truth → Facts
Historical confirmed event → Timeline
Raw evidence → Records
Confirmed decision → Decisions
How-to instruction → Rules
Repeated verified pattern → Learnings
One-off event with result → Case
External uncertain info → Research
Work in progress → Project / Draft
System principle → Core
High-risk update → Proposal
Unclear content → Inbox
```

## 23.2 Check SSOT

Before writing formal knowledge:

```text
Is there an existing authority file?
If yes, do not create parallel truth.
If no, use Source of Truth System.
If unknown, write to Inbox.
```

## 23.3 Check Permission

```text
Class A → proposal only
Class B → create/append, proposal for key changes
Class C → open write
Class R → append-only evidence
```

## 23.4 Write or Propose

```text
Fast-write area → write directly
Records area → append with metadata
Controlled area → create proposal
Unknown area → Inbox
```

---

# 24. Knowledge Promotion Framework

Knowledge may be promoted, but only through correct paths.

Wrong model:

```text
Draft → Research → Learning → Rule → Core
```

Correct model:

```text
Draft / Inbox / Project / Record
↓
Triage
↓
Facts / Rules / Cases / Research / Records / Projects / Proposal
↓
Validated Learning where appropriate
↓
Reusable Rule where appropriate
↓
Core only if system-level and stable
```

## 24.1 Draft to Facts

Requires:

- source
- owner
- no SSOT conflict
- approval if high-risk

## 24.2 Record to Facts

Requires:

- Record remains append-only
- Fact update through proposal where required
- source link to Record
- changelog or timeline entry

## 24.3 Draft to Research

Requires:

- source
- confidence
- review_date
- expires_at or freshness class

## 24.4 Project to Case

Requires:

- completed project
- clear action
- clear result
- evidence

## 24.5 Case to Learning

Requires at least one:

- multiple supporting cases
- multiple customers
- clear data
- human confirmation
- failure comparison
- repeated successful use

## 24.6 Learning to Rule

Requires:

- repeatability
- clear trigger
- clear steps
- clear output standard
- exceptions
- approval

## 24.7 Rule to Core

Allowed only if:

- system-level
- stable
- cross-project
- cross-agent
- highly abstract
- not business-detail-specific
- approved

---

# 25. Conflict Resolution Policy

Conflicts are expected.

The system must not hide them.

## 25.1 Authority Priority

Default priority:

```text
1. Core Memory, only for system principles
2. Approved Rules, only for execution standards
3. Domain Facts SSOT
4. Historical confirmed facts
5. Source Records
6. Approved Learnings
7. Reviewed Research
8. Active project notes
9. Raw Research
10. Proposals
11. Drafts / Inbox
12. Logs
13. Archive, only for historical tracing
```

Core does not override product, brand, or customer facts.

Facts SSOT wins for domain truth.

Records support facts but do not override approved facts by default.

## 25.2 Conflict Handling

When conflict is found:

1. Do not delete original evidence
2. Find relevant SSOT
3. Identify conflicting sources
4. Create conflict proposal
5. Recommend resolution
6. Mark uncertain content
7. Add changelog after approval
8. Mark lower-authority content outdated or superseded where appropriate

## 25.3 Conflict Note Location

```text
93-Proposals/Conflicts/
```

or:

```text
94-Review-Queues/Conflict-Queue.md
```

---

# 26. Permission Model

The system uses four permission classes.

## 26.1 Class A — Core Assets

Includes:

- Core Memory
- Source of Truth System
- Brand Facts
- Product Facts
- Approved Rules
- Agent behavior rules
- Permission Policy
- Retrieval Rules
- Context Packing Policy
- Schema Policy
- Security Policy

Policy:

```text
read by default
proposal only for changes
human approval required
changelog required
source required
```

Hermes must not overwrite Class A files directly.

## 26.2 Class B — Knowledge Assets

Includes:

- customer files
- timelines
- decisions
- cases
- learnings
- reviewed notes
- research
- projects

Policy:

```text
Hermes may create or append
key current-state changes require proposal
learning approval requires review
customer profile changes require review
```

## 26.3 Class C — Temporary Assets

Includes:

- drafts
- inbox
- logs
- proposals
- review queues
- project working drafts
- research inbox

Policy:

```text
open write
low authority
excluded from default retrieval
subject to lifecycle cleanup
```

## 26.4 Class R — Records Assets

Includes:

- meetings
- calls
- emails
- feedback
- transcripts
- imports
- source materials

Policy:

```text
append-only
correction by new note
not current truth by default
evidence role
sensitive data policy applies
```

## 26.5 Emergency Override

Emergency override may apply only to limited Class B current workflow updates.

It must not apply to:

- Core
- Brand
- Product facts
- Approved Rules
- Security Policy
- Permission Policy

Emergency writes must include:

- `status: needs_review`
- source
- reason
- timestamp
- review deadline

---

# 27. Write Speed Policy

The system separates speed from authority.

## 27.1 Fast Path

Allowed:

- Drafts
- Inbox
- Logs
- project notes
- research inbox
- proposals

Properties:

- fast
- low authority
- no default retrieval
- lifecycle cleanup

## 27.2 Records Path

Allowed:

- meeting notes
- emails
- calls
- transcripts
- raw feedback
- imported documents

Properties:

- append-only
- evidence role
- not current truth
- can trigger proposal

## 27.3 Controlled Path

Requires approval:

- Core
- Brand
- Products
- Rules
- Customer profile current state
- Learnings approval
- Reviewed Research
- Source of Truth System
- Security Policy
- Permission Policy
- Retrieval Policy

Properties:

- slow
- high authority
- source required
- changelog required
- proposal required

---

# 28. Memory Write Pipeline

Formal memory must flow through a controlled pipeline.

```text
Hermes through Claudian runtime
↓
Draft / Inbox / Project / Research Inbox / Record / Proposal
↓
Triage
↓
Review where required
↓
Promote
↓
Merge into SSOT
↓
Changelog
↓
Index / dashboard update where needed
```

## 28.1 Create

Hermes creates content in allowed write areas.

## 28.2 Triage

Hermes classifies knowledge and recommends destination.

## 28.3 Review

Only required for high-authority impact.

## 28.4 Promote

Content moves to the correct formal layer.

## 28.5 Merge

If SSOT exists:

- update target authority file only after permission is satisfied
- add changelog
- cite source
- archive proposal
- update index if needed

---

# 29. Agent Write Rules

Hermes must follow these rules.

## 29.1 Determine Type

```text
Fact?
Rule?
Learning?
Case?
Research?
Record?
Project material?
Draft?
Log?
Proposal?
```

## 29.2 Determine SSOT

If authority exists, do not create another authority file.

## 29.3 Determine Permission

Class A → proposal only  
Class B → create/append with constraints  
Class C → open write  
Class R → append-only

## 29.4 Determine Expiration

Must have review_date or expires_at:

- research
- market data
- platform rules
- pricing
- competitor information
- volatile product facts
- approved rules
- learnings

## 29.5 Determine Source Requirement

Source required for:

- facts
- rules
- research
- records
- learnings
- decisions
- proposals
- customer profile changes
- product changes
- brand changes

No-source content goes to Draft or Inbox.

## 29.6 Determine Sensitivity

Sensitive content includes:

- credentials
- API keys
- private customer data
- personal identifiers
- financial information
- legal information
- confidential strategy

Sensitive content must follow Security and Retention Policy.

---

# 30. Retrieval Runtime Architecture

Retrieval must be conservative by default.

The system optimizes for reliable memory, not maximum recall.

## 30.1 Retrieval Modes

```yaml
retrieval_modes:
  - exact_ssot_lookup
  - source_of_truth_lookup
  - metadata_filter_search
  - semantic_search
  - backlink_expansion
  - recency_boosted_search
  - authority_boosted_search
  - project_context_search
  - evidence_trace_search
  - historical_trace_search
  - conflict_search
  - debug_log_search
```

## 30.2 Default Retrieval Flow

```text
1. Identify task type
2. Select retrieval preset
3. Check Source of Truth System
4. Exact lookup for known SSOT
5. Metadata-filtered search
6. Semantic search only within allowed layers
7. Apply ranking and exclusions
8. Pack context
9. Answer or act
10. Report sources for high-risk answers
```

## 30.3 Writing Retrieval Flow

Before formal write:

```text
1. Load Core principle if relevant
2. Load Source of Truth Map
3. Load Permission Policy
4. Load relevant schema
5. Load target SSOT
6. Load active proposal if exists
7. Load evidence records only as needed
8. Write proposal or allowed update
```

## 30.4 Evidence Retrieval Flow

When verifying fact origin:

```text
1. Load current SSOT
2. Load changelog
3. Follow source links
4. Load relevant Records
5. Check timestamps
6. Check newer conflicting evidence
7. Return current fact and evidence trail
```

## 30.5 Historical Retrieval Flow

```text
1. Load timeline
2. Load records
3. Load archive only if required
4. Load superseded files if relevant
5. Mark output historical
6. Do not update current truth without proposal
```

---

# 31. Retrieval Ranking and Scoring

Ranking should not depend only on semantic similarity.

## 31.1 Recommended Formula

```text
final_score =
  semantic_relevance
+ authority_weight
+ ssot_weight
+ task_match_weight
+ source_quality_weight
+ freshness_weight
+ project_relevance_weight
+ backlink_weight
- stale_penalty
- draft_penalty
- archive_penalty
- deprecated_penalty
- conflict_penalty
- security_penalty
```

## 31.2 Simple Stable Priority

For early and low-maintenance operation, use:

```text
Exact SSOT
> Approved Rules
> Current Facts
> Active Project Context
> Approved Learnings
> Reviewed Research
> Records only when evidence is needed
> Drafts / Inbox / Logs / Archive excluded
```

## 31.3 Authority Weights

```yaml
authority_weight:
  ssot: 100
  approved: 80
  reference: 50
  provisional: 25
  raw: 15
  none: 0
```

## 31.4 Layer Weights

```yaml
layer_weight:
  core: 100
  facts: 95
  rules: 90
  insights_approved: 65
  research_reviewed: 50
  projects_active: 45
  records_evidence_only: 35
  research_raw: 20
  proposals: 10
  drafts: -50
  logs: -70
  archive: -80
```

## 31.5 Default Exclusion

Exclude by default:

```text
status: archived
status: deprecated
status: superseded
status: rejected
memory_layer: draft
memory_layer: inbox
memory_layer: logs
memory_layer: proposal
memory_layer: archive
raw research
records unless evidence mode
```

---

# 32. Context Packing Policy

Context packing determines what memory enters the model context.

## 32.1 Context Tiers

```text
Tier 0: User request and task instruction
Tier 1: Exact SSOT files
Tier 2: Relevant approved rules
Tier 3: Relevant current facts
Tier 4: Active project context
Tier 5: Approved learnings
Tier 6: Reviewed research summaries
Tier 7: Source records / evidence excerpts
Tier 8: Raw research / drafts / archive only when explicitly needed
```

## 32.2 Packing Rules

Hermes should not load the entire Vault.

Default loading:

```text
1. Minimal Core principles
2. Exact relevant SSOT
3. Relevant approved rules
4. Active project context if applicable
5. Evidence only when needed
```

## 32.3 Summarize vs Load

Load full text:

- target SSOT file
- short approved rule
- active proposal
- customer profile
- project brief

Summarize:

- long research
- long transcripts
- large project histories
- archived material
- logs

Load pointer only:

- unrelated indexes
- old drafts
- superseded files
- low-quality raw research

## 32.4 Context Budget

Recommended:

```yaml
context_budget:
  task_instruction: 10%
  exact_ssot: 30%
  rules: 20%
  project_context: 15%
  evidence: 15%
  research_or_insights: 10%
```

High-risk write tasks may increase SSOT and evidence.

Research tasks may increase reviewed research but must not treat research as fact.

---

# 33. Retrieval Filter Presets

## 33.1 Default Execution Retrieval

Include:

```yaml
memory_layer:
  - core
  - facts
  - rules
  - insights_approved
  - research_reviewed
  - projects_active_when_relevant
status:
  - active
  - approved
authority:
  - ssot
  - approved
  - reference
```

Exclude:

```yaml
memory_layer:
  - draft
  - inbox
  - logs
  - proposal
  - archive
  - records_unless_evidence
  - research_raw
status:
  - draft
  - archived
  - deprecated
  - superseded
  - rejected
  - expired
```

## 33.2 Writing Retrieval

Must include:

```text
Core principle if relevant
Source-of-Truth-Map
Permission-Policy
Relevant schema
Relevant SSOT file
Relevant proposal if exists
```

Optional:

```text
Relevant Records
Timeline
Changelog
```

## 33.3 Research Retrieval

Priority:

```text
Reviewed Research
Reference
Current Facts
Approved Rules
Raw Research with low-authority warning
External sources
```

## 33.4 Evidence Retrieval

Include:

```text
Facts SSOT
Changelog
Decisions
Records
Timeline
Approved source references
```

Output must distinguish:

```text
Current fact
Supporting evidence
Historical note
Unresolved conflict
```

## 33.5 Historical Retrieval

Include:

```text
Archive
Timeline
Records
Old projects
Superseded files
```

All output must be marked historical.

## 33.6 Debug Retrieval

Include:

```text
Logs
Automation notes
Error reports
Related SOPs
```

Logs are diagnostic only.

---

# 34. Knowledge Graph Metadata

Metadata enables retrieval, audit, lifecycle, and automation.

## 34.1 Minimal Required Metadata

For formal files:

```yaml
type:
memory_layer:
status:
authority:
source:
updated:
write_policy:
```

## 34.2 Extended Metadata

Use when applicable:

```yaml
owner:
created:
review_date:
expires_at:
confidence:
source_quality:
approved_by:
reviewer:
last_verified:
retrieval_scope:
sensitivity:
retention_until:
schema:
related:
tags:
canonical_id:
superseded_by:
```

## 34.3 Field Definitions

### type

```yaml
type: product
type: customer_profile
type: decision
type: rule
type: case
type: learning
type: research
type: project
type: record
type: proposal
type: index
type: dashboard
type: log
```

### memory_layer

```yaml
memory_layer: core
memory_layer: facts
memory_layer: rules
memory_layer: insights
memory_layer: research
memory_layer: projects
memory_layer: records
memory_layer: draft
memory_layer: inbox
memory_layer: logs
memory_layer: proposal
memory_layer: archive
```

### status

```yaml
status: draft
status: active
status: needs_review
status: deprecated
status: archived
status: superseded
status: pending
status: approved
status: rejected
status: applied
status: expired
```

### authority

```yaml
authority: ssot
authority: approved
authority: reference
authority: provisional
authority: raw
authority: none
```

### source_quality

```yaml
source_quality: user_confirmed
source_quality: primary_source
source_quality: internal_record
source_quality: external_official
source_quality: external_secondary
source_quality: ai_generated
source_quality: unknown
```

### write_policy

```yaml
write_policy: review_required
write_policy: append_only
write_policy: open
write_policy: read_only
write_policy: proposal_only
```

### sensitivity

```yaml
sensitivity: public
sensitivity: internal
sensitivity: confidential
sensitivity: restricted
sensitivity: secret
```

### retrieval_scope

```yaml
retrieval_scope: default
retrieval_scope: evidence_only
retrieval_scope: historical_only
retrieval_scope: debug_only
retrieval_scope: excluded
```

## 34.4 Example Metadata

```yaml
---
type: product
memory_layer: facts
status: active
authority: ssot
owner: human
created: 2026-01-01
updated: 2026-06-05
review_date: 2026-12-01
source:
  - founder-confirmed
source_quality: user_confirmed
confidence: high
write_policy: review_required
approved_by: human
sensitivity: internal
retrieval_scope: default
schema: product.schema.yml
related:
  - 02-Rules/SEO/SEO-Content-Rule.md
  - 03-Insights/Cases/Example-Case.md
tags:
  - product
---
```

---

# 35. Schema Validation Layer

Location:

```text
70-Schemas/
```

Purpose: make governance checkable

Recommended schemas:

```text
70-Schemas/
  product.schema.yml
  customer_profile.schema.yml
  rule.schema.yml
  learning.schema.yml
  research.schema.yml
  record.schema.yml
  decision.schema.yml
  proposal.schema.yml
  project_closeout.schema.yml
```

## 35.1 Validation Checks

Check for:

- missing required metadata
- missing source
- missing owner where required
- invalid authority
- invalid memory_layer
- Class A change without proposal
- Class A file without changelog
- research without freshness class or review_date
- rule without exceptions
- learning without evidence
- record without sensitivity
- superseded file without superseded_by
- archived file in default retrieval
- customer profile modified without proposal
- product file modified without proposal

## 35.2 Failure Handling

```text
Class A schema failure → block direct write and create proposal
Class B schema failure → allow draft or needs_review
Class C schema failure → allow write and add cleanup queue
Class R schema failure → allow append if urgent and mark needs_metadata
```

## 35.3 Example Product Schema

```yaml
schema: product
required:
  - type
  - memory_layer
  - status
  - authority
  - updated
  - source
  - source_quality
  - write_policy
  - review_date
  - approved_by
rules:
  type: product
  memory_layer: facts
  authority: ssot
  write_policy: review_required
  changelog_required: true
```

---

# 36. Changelog Requirement

All Class A files require changelog.

Recommended format:

```markdown
## Changelog

| Date | Change | Source | Proposal | Approved By |
|---|---|---|---|---|
| 2026-06-05 | Updated product positioning | Founder note | 93-Proposals/Facts/... | Human |
```

Class B files should have changelog when they affect future behavior or current state.

Class R uses correction log or append-only notes.

Class C does not require changelog.

---

# 37. Naming Convention

Consistent naming prevents duplication.

## 37.1 General Rules

- use clear names
- avoid `final`, `new`, `copy`, `v2`
- dates use `YYYY-MM-DD`
- one authority entity, one file
- historical change uses changelog or timeline
- raw records use date and source

## 37.2 Naming Patterns

```text
Products: Product-Name.md
Brand: Positioning.md / Tone-of-Voice.md
Customer profile: profile.md
Timeline: YYYY.md
Meeting records: YYYY-MM-DD-Customer-Topic.md
Email records: YYYY-MM-DD-From-To-Topic.md
Call records: YYYY-MM-DD-Customer-Topic.md
Decisions: YYYY-MM-DD-Decision-Name.md
Rules: Domain-Rule-Name.md
Research: YYYY-MM-DD-Topic.md
Cases: YYYY-MM-DD-Case-Name.md
Learnings: Domain-Learnings.md
Projects: YYYY-Client-Project-Name/
Proposals: YYYY-MM-DD-Target-Change.md
Logs: YYYY-MM-DD-Agent-Task.md
```

---

# 38. File Lifecycle

All formal memory must have lifecycle status.

## 38.1 draft

Unapproved working material.

Excluded from default retrieval.

## 38.2 active

Current and usable.

Can participate in default retrieval if allowed by layer.

## 38.3 needs_review

May be useful but not final.

Use cautiously.

## 38.4 deprecated

No longer recommended.

Excluded from default retrieval.

## 38.5 archived

Historical only.

Excluded from default retrieval.

## 38.6 superseded

Replaced by another file.

Must include:

```yaml
superseded_by:
superseded_reason:
superseded_date:
```

## 38.7 expired

Automatically expired due to lifecycle rules.

Excluded from default retrieval.

---

# 39. Automatic Lifecycle Rules

V7.1 Stable reduces maintenance through automatic lifecycle rules.

## 39.1 Drafts

```text
30 days unused → stale
90 days unused → archive candidate
180 days unused → archive automatically unless pinned
```

## 39.2 Inbox

```text
14 days unclassified → Hermes auto-classifies if possible
30 days unresolved → move to 99-Archive/Unsorted/ or keep as low-authority archived note
```

## 39.3 Raw Research

```text
volatile_30d → review after 30 days
normal_90d → review after 90 days
stable_180d → review after 180 days
evergreen_365d → review after 365 days
```

If not promoted or renewed:

```text
stale → archive after additional 90 days
```

## 39.4 Projects

```text
30 days no activity → inactive
90 days no activity → closeout candidate
180 days no activity → archive unless pinned active
```

## 39.5 Logs

```text
30 days active diagnostic value
90 days archive or delete unless linked to incident
```

## 39.6 Proposals

```text
30 days pending → reminder
90 days pending → auto-expired unless marked critical
Expired proposals do not participate in default retrieval
```

## 39.7 Records

Records are append-only and retained according to Security and Retention Policy.

Records do not automatically promote to Facts.

---

# 40. Review and Audit

V7.1 Stable uses low-frequency, high-impact review.

## 40.1 Review by Exception

Review only items that affect:

- current truth
- customer current state
- product facts
- brand facts
- approved rules
- Core principles
- security posture
- permission model
- retrieval behavior
- major conflicts

## 40.2 Monthly Knowledge Review

Optional but recommended.

Check:

- pending high-risk proposals
- conflict queue
- stale research with high usage
- project closeout candidates
- duplicate authority candidates
- schema failures in Class A or high-risk Class B

Output:

```text
94-Review-Queues/Monthly-Review-Queue.md
```

## 40.3 Quarterly Architecture Audit

Should not redesign architecture.

Check:

- SSOT integrity
- archive leakage
- retrieval contamination
- permission violations
- stale high-authority knowledge
- schema pass rate
- security retention issues

Output:

```text
81-Dashboards/Quarterly-Audit.md
```

---

# 41. Low-Maintenance Operations

The system is optimized to avoid constant manual maintenance.

## 41.1 Human Review Scope

Humans only need to review:

```text
1. Does this change current truth?
2. Does this change future behavior?
3. Does this affect customer/product/brand/security?
4. Does this resolve a conflict?
5. Should this low-authority memory be promoted?
```

Humans should not manually manage every draft, log, raw research note, or record.

## 41.2 Hermes Responsibilities

Hermes should automatically:

- classify new content
- write records
- create drafts
- generate proposals
- detect duplicate candidates
- detect stale research
- detect schema failures
- generate review summaries
- recommend archive actions
- summarize project closeout candidates

## 41.3 Low-Maintenance Rule

```text
Do not ask for human review unless the change affects authority.
```

---

# 42. Knowledge Debt Dashboard

Location:

```text
81-Dashboards/Knowledge-Debt-Dashboard.md
```

Tracks:

- Inbox count
- drafts older than 30 days
- stale research
- missing source
- missing owner in formal files
- schema failures
- open conflicts
- pending proposals
- expired proposals
- projects without closeout
- records awaiting promotion
- superseded files missing pointer
- archive leakage
- sensitive records without retention metadata

Knowledge debt must be visible.

Invisible debt eventually pollutes retrieval.

---

# 43. Memory Evaluation Metrics

Location:

```text
81-Dashboards/Memory-Evaluation-Dashboard.md
```

Core metrics:

```text
Memory Precision
Memory Recall
Stale Knowledge Rate
Duplicate Knowledge Rate
Proposal Aging
Review Debt
Retrieval Contamination Rate
Answer Attribution Rate
SSOT Lookup Success Rate
Schema Pass Rate
Records Promotion Rate
Archive Leakage Rate
```

## 43.1 Definitions

Memory Precision: retrieved memory that was relevant and usable.

Memory Recall: needed memory successfully found.

Stale Knowledge Rate: answers using expired or outdated memory.

Duplicate Knowledge Rate: same knowledge appearing as multiple authority candidates.

Retrieval Contamination Rate: Drafts, Raw Research, Logs, Records, or Archive used as current truth incorrectly.

Answer Attribution Rate: high-risk answers that report memory sources.

SSOT Lookup Success Rate: ability to find authoritative truth when needed.

Archive Leakage Rate: archived material appearing in default retrieval.

## 43.2 Low-Maintenance Evaluation

If full metrics are too heavy, track only:

```text
SSOT Lookup Success
Retrieval Contamination
Stale High-Authority Knowledge
Pending High-Risk Proposals
Archive Leakage
```

---

# 44. Security, Privacy, and Retention Policy

Location:

```text
00-Core/Security-and-Retention-Policy.md
```

## 44.1 Sensitive Data

Sensitive data includes:

- credentials
- API keys
- passwords
- private customer information
- personal identifiers
- financial information
- legal information
- confidential strategy
- regulated information

## 44.2 Rules

- Do not store secrets in normal notes.
- Do not store raw credentials in Vault.
- Sensitive records require `sensitivity` metadata.
- Sensitive records require `retention_until` where applicable.
- Sensitive records should be excluded from default retrieval unless needed.
- Logs containing sensitive data must be redacted or restricted.

## 44.3 Retention

Retention should be defined by sensitivity:

```yaml
public: normal lifecycle
internal: normal lifecycle
confidential: review retention annually
restricted: explicit retention_until required
secret: do not store in normal Vault
```

## 44.4 Deletion vs Archive

Archive preserves historical context.

Deletion removes data.

Sensitive data may require deletion instead of archive.

---

# 45. Backup and Recovery Policy

Location:

```text
00-Core/Backup-and-Recovery-Policy.md
```

Recommended:

- Git version history for text files
- regular Vault backup
- encrypted backup for sensitive data
- test restore process
- preserve changelog and proposal history

Minimum recovery requirements:

```text
Can restore Core
Can restore Facts
Can restore Rules
Can restore Records
Can restore Archive
Can inspect history of Class A changes
```

---

# 46. Standard Templates

Templates should live in:

```text
70-Schemas/Templates/
```

or:

```text
00-Core/Templates/
```

Recommended templates:

- Product Fact Template
- Customer Profile Template
- Decision Template
- Rule Template
- Case Template
- Learning Template
- Research Template
- Record Template
- Proposal Template
- Conflict Note Template
- Project Closeout Template

## 46.1 Proposal Template

```markdown
---
type: proposal
memory_layer: proposal
status: pending
authority: none
source:
updated:
write_policy: open
proposal_type:
target_file:
risk:
---

# Proposal: {Title}

## Target File

## Proposed Change

## Reason

## Source Evidence

## Risk

## Affected Files

## Suggested Changelog Entry

## Rollback Plan

## Reviewer Decision

- [ ] Approved
- [ ] Rejected
- [ ] Needs Revision
- [ ] Expired
```

## 46.2 Record Template

```markdown
---
type: record
memory_layer: records
status: active
authority: raw
source:
source_quality: internal_record
created:
updated:
write_policy: append_only
sensitivity: internal
retrieval_scope: evidence_only
---

# {Date} {Source} {Topic}

## Summary

## Raw Notes / Evidence

## Potential Follow-up

## Possible Promotions

- [ ] Decision proposal
- [ ] Customer profile proposal
- [ ] Timeline append
- [ ] Case
- [ ] Learning candidate
- [ ] Research
```

## 46.3 Rule Template

```markdown
---
type: rule
memory_layer: rules
status: active
authority: approved
source:
source_quality:
owner:
updated:
review_date:
write_policy: review_required
retrieval_scope: default
---

# Rule: {Name}

## Purpose

## Scope

## Trigger / Input

## Steps

## Output Standard

## Quality Standard

## Exceptions

## Prohibited Actions

## Related Facts

## Related Cases / Learnings

## Changelog
```

---

# 47. Claudian Skills and Workflows

Recommended skills:

```text
/triage-note
/create-record
/create-proposal
/check-ssot
/check-permission
/promote-record
/closeout-project
/check-schema
/check-stale-research
/detect-duplicates
/generate-review-summary
/archive-expired
```

## 47.1 Skill Rules

Skills must respect:

- Permission Model
- SSOT System
- default retrieval exclusions
- schema validation
- security policy
- lifecycle rules

Skills may automate operations.

Skills may not bypass authority.

---

# 48. Automation and Enforcement

Automation should enforce architecture without requiring daily manual review.

Recommended automation:

- metadata validation
- stale research detection
- archive leakage detection
- duplicate authority detection
- schema failure queue
- proposal aging
- project inactivity detection
- log retention cleanup
- draft expiration
- inbox auto-triage

## 48.1 Enforcement Priority

Highest priority:

```text
Prevent Class A direct writes
Prevent Archive in default retrieval
Prevent Draft/Inbox/Logs as current truth
Prevent Records as current facts
Prevent missing source in Facts/Rules/Research
Prevent sensitive data leakage
```

---

# 49. Human Review UX

Human review should be simple.

Each review item should ask:

```text
Approve?
Reject?
Needs revision?
Expire?
```

Review cards should show:

- proposed change
- target file
- current authority
- source evidence
- risk
- affected files
- Hermes recommendation

The reviewer should not need to inspect the entire Vault.

Hermes should prepare the context.

---

# 50. Failure Modes and Recovery

## 50.1 Failure: Proposal Backlog

Cause: too many review requirements.

Recovery:

- expire old proposals
- review only high-authority items
- auto-archive low-risk suggestions
- merge duplicate proposals

## 50.2 Failure: Records Never Promoted

Cause: capture without triage.

Recovery:

- promote only high-impact records
- use timeline append for minor history
- leave most records as evidence

## 50.3 Failure: Drafts Pollute Retrieval

Cause: Drafts included in search.

Recovery:

- enforce retrieval_scope exclusion
- archive old drafts
- audit retrieval preset

## 50.4 Failure: Research Becomes Fact

Cause: answers cite research as current truth.

Recovery:

- require distinction between Facts and Research
- move unreviewed research out of default retrieval
- add freshness class

## 50.5 Failure: Archive Leakage

Cause: archived content appears in default retrieval.

Recovery:

- set retrieval_scope: historical_only
- add archive penalty
- validate search filters

## 50.6 Failure: Schema Ignored

Cause: schema too heavy.

Recovery:

- enforce minimal metadata first
- apply strict schema only to Class A
- queue failures instead of blocking low-risk writes

## 50.7 Failure: Architecture Drift

Cause: ad-hoc folders and new layers.

Recovery:

- freeze top-level structure
- route new domains into existing layers
- create proposal for architecture-level changes

---

# 51. Operating Cadence

V7.1 Stable minimizes operational burden.

## 51.1 Daily

No required daily review.

Hermes may write:

- records
- drafts
- project notes
- logs
- proposals

## 51.2 Weekly

Optional 15-30 minutes if active usage is high.

Review:

- high-risk proposals
- major conflicts
- customer current-state changes
- product or rule change proposals

## 51.3 Monthly

Recommended 30-60 minutes.

Review:

- stale high-value research
- project closeout candidates
- duplicate authority candidates
- Class A schema failures
- security review queue

## 51.4 Quarterly

Recommended architecture health check.

Do not redesign structure unless necessary.

Check:

- SSOT integrity
- retrieval contamination
- archive leakage
- permission violations
- high-authority stale knowledge

---

# 52. Migration / Deployment Plan

V7.1 Stable is intended for one-time deployment.

## 52.1 Initial Deployment

Create full folder structure:

```text
00-Core/
01-Facts/
02-Rules/
03-Insights/
04-Research/
05-Projects/
06-Records/
70-Schemas/
80-Indexes/
81-Dashboards/
90-Drafts/
91-Inbox/
92-Logs/
93-Proposals/
94-Review-Queues/
99-Archive/
```

Create Core files:

```text
Core-Memory.md
Hermes-Operating-Protocol.md
Source-of-Truth-Map.md
Permission-Policy.md
Retrieval-Rules.md
Context-Packing-Policy.md
Knowledge-Triage-Rules.md
Conflict-Resolution-Policy.md
Security-and-Retention-Policy.md
Lifecycle-Policy.md
```

Create minimum templates:

```text
Record Template
Proposal Template
Rule Template
Customer Profile Template
Product Template
Research Template
Project Closeout Template
```

## 52.2 Initial Enforcement

Immediately enforce:

- no Drafts in default retrieval
- no Archive in default retrieval
- Records are evidence only
- Class A proposal only
- basic metadata on formal files
- source required for Facts / Rules / Research / Records / Proposals

## 52.3 No Future Redeployment

Future work should only:

- add files
- add subfolders
- refine templates
- improve automation
- tune schemas
- improve dashboards

Do not change top-level architecture unless workspace purpose changes fundamentally.

---

# 53. Success Criteria

The system succeeds if:

- current truth is easy to find
- source evidence can be traced
- Drafts do not become truth
- Records do not become current facts by accident
- Research does not become fact by accident
- Archive does not pollute default retrieval
- AI can write freely in low-authority areas
- AI cannot silently modify high-authority truth
- human review is needed only for important changes
- project knowledge is extracted or archived
- stale memory is degraded or archived automatically
- the architecture does not require structural redesign over time

---

# 54. Ultimate Principle

The workspace does not optimize for remembering everything.

It optimizes for preserving only governed, source-backed, reviewable, and useful memory.

AI may generate, classify, summarize, capture, archive, and propose.

AI may not silently convert uncertain information into facts, rules, or core memory.

Truth is defined by SSOT files.

Evidence is preserved in Records.

Authority is controlled by Permission Model.

Retrieval is conservative by default.

Unreviewed memory expires, degrades, or archives automatically.

Only changes that affect current truth or future behavior require human approval.

The architecture is deployed once.

The content evolves continuously.

The system must remain stable, auditable, controllable, and low-maintenance.


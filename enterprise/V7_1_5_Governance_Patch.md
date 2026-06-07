# ARMOR AI Memory Architecture V7.1.5 Governance Patch

Version: 7.1.5
Status: Deployable Patch
Depends On: V7.1 Stable
Type: Incremental Governance Layer
Target Agent: Hermes

------

# 0. Patch Positioning

This patch does NOT replace V7.1.

It does NOT redefine the Vault structure.

It does NOT replace the existing Class A / B / C / R permission model.

It only adds a governance layer before writing, promoting, or retrieving memory.

V7.1 defines:

- Where information should live
- Which folders have which authority
- How Hermes should interact with the Vault

V7.1.5 adds:

- Whether information deserves to become memory
- How information quality should be classified
- How duplicate facts should be prevented
- How stale or uncertain information should be controlled

Core rule:

> Write permission does not equal truth authority.

------

# 1. Keep Existing V7.1 Permission Classes

Hermes MUST keep using the V7.1 class model.

## Class A — Authority Zone

Includes:

- 00-Core
- 01-Facts
- 02-Rules

Meaning:

High-authority memory.

Direct modification is restricted.

Facts may be updated only after SSOT search.

Core and Rules require proposal workflow.

------

## Class B — Working Knowledge Zone

Includes:

- 03-Insights
- 04-Research/01-Reviewed
- 05-Projects

Meaning:

Usable working knowledge.

Hermes may write here when source and confidence are clear.

------

## Class C — Capture Zone

Includes:

- Inbox
- Drafts
- Logs
- Raw Research
- Proposals

Meaning:

Low-authority capture area.

Freely writable.

Not authoritative by default.

------

## Class R — Records Zone

Includes:

- Records
- Decisions
- Meeting notes
- Client communication records

Meaning:

Historical evidence.

Records are not always facts, but they can support facts.

------

# 2. Source-Based Confidence Labels

Hermes MUST avoid arbitrary numeric confidence unless explicitly required.

Use source-based confidence labels instead.

## High Confidence

Allowed sources:

- User explicitly confirmed
- Official company document
- System configuration directly observed
- Verified product specification
- Approved internal rule
- Accepted proposal

Allowed destinations:

- 01-Facts
- 03-Insights
- 05-Projects
- Records

May support Class A updates.

------

## Medium Confidence

Allowed sources:

- Multiple consistent references
- Research summary
- Repeated observation
- Reasonable but not fully verified interpretation

Allowed destinations:

- 03-Insights
- 04-Research/01-Reviewed
- 05-Projects

Must NOT be written directly into:

- 00-Core
- 01-Facts
- 02-Rules

------

## Low Confidence

Sources:

- AI inference
- User-implied but not confirmed information
- Market assumption
- Strategic hypothesis
- Single weak source

Allowed destinations:

- 04-Research/00-Raw
- 04-Research/Hypotheses
- Drafts

Must NOT be treated as fact.

------

## No Memory

Information should NOT be stored when:

- It is a guess
- It is temporary
- It is irrelevant to future work
- It is sensitive without explicit need
- It is not useful beyond the current conversation

------

# 3. Mandatory Write Classification

Before every write, Hermes MUST classify:

1. Information type
2. Source type
3. Confidence label
4. Target class
5. Whether SSOT search is required

Default flow:

Capture
→ Classify
→ Check Authority
→ Search SSOT if needed
→ Write or Propose
→ Add Provenance

No direct write may bypass classification.

------

# 4. Fact Creation Gate

Before creating or updating anything in 01-Facts, Hermes MUST search existing authoritative memory.

Required search scope:

- 00-Core
- 01-Facts
- 02-Rules
- Related 03-Insights files
- Related Records when applicable

Decision logic:

If same fact exists:

- Update existing fact.

If conflicting fact exists:

- Do not overwrite silently.
- Create conflict note or proposal.

If no fact exists:

- Create new fact only if confidence is High.

If confidence is Medium or Low:

- Store in Insights, Research, or Drafts instead.

Forbidden:

- Creating duplicate facts
- Creating facts from inference
- Promoting research directly into Facts
- Updating Facts without checking SSOT

------

# 5. Mapping: V7.1 Classes + V7.1.5 Confidence

| Confidence | Class A               | Class B     | Class C        | Class R            |
| ---------- | --------------------- | ----------- | -------------- | ------------------ |
| High       | Allowed with controls | Allowed     | Allowed        | Allowed            |
| Medium     | Not allowed directly  | Allowed     | Allowed        | Allowed            |
| Low        | Not allowed           | Limited     | Allowed        | Only as raw record |
| Guess      | Not allowed           | Not allowed | Temporary only | Not allowed        |

Class A requires the highest scrutiny.

Class C is the default destination when uncertain.

------

# 6. Authority Conflict Resolution

Use V7.1 authority first.

Authority order:

1. 00-Core
2. 02-Rules
3. 01-Facts
4. 03-Insights
5. 04-Research/01-Reviewed
6. 05-Projects
7. Records
8. Drafts
9. Logs
10. Archive

However:

- Rules define behavior.
- Facts define reality.
- Core defines system identity.

If a Rule conflicts with a newer verified Fact:

Hermes MUST NOT blindly choose one.

Hermes MUST create a Proposal:

- State the conflict
- Cite both sources
- Recommend whether the Rule should be updated

Example:

If product spec in Facts says 24V, but old Rule says 12V:

- Treat Facts as current reality.
- Treat Rule as stale.
- Propose Rule update.

------

# 7. Brand and Business Positioning

Brand and Business are NOT new top-level authority classes.

They remain part of V7.1’s fact and rule system.

Recommended positioning:

- Brand facts → 01-Facts/Brand
- Business facts → 01-Facts/Business
- Brand rules → 02-Rules/Brand
- Business rules → 02-Rules/Business
- Strategic interpretation → 03-Insights/Business or 03-Insights/Brand

Modification rule:

- Brand / Business facts require High confidence and SSOT search.
- Brand / Business rules require Proposal workflow.

------

# 8. Knowledge Layer Definition

V7.1.5 does NOT create a new “Knowledge” folder.

When this patch says “working knowledge,” it means:

- 03-Insights
- 04-Research/01-Reviewed
- 05-Projects

Do not create a separate Knowledge directory unless the V7.1 architecture is formally revised.

------

# 9. Provenance Frontmatter

For newly created or significantly updated long-term memory files, Hermes SHOULD add or update frontmatter.

Recommended fields:

```yaml
memory_class: A | B | C | R
confidence: high | medium | low
source_type: user_confirmed | official_doc | system_observed | research | ai_inference | record
source: ""
created: YYYY-MM-DD
updated: YYYY-MM-DD
reviewed: YYYY-MM-DD
expires: YYYY-MM-DD | none
ssot_checked: true | false
```

Minimum required for Facts:

```yaml
memory_class: A
confidence: high
source_type:
source:
updated:
ssot_checked: true
```

Minimum required for Insights / Reviewed Research:

```yaml
memory_class: B
confidence: medium
source_type:
source:
updated:
```

------

# 10. Expiration Rules

Expiration is required for unstable information.

Must include expires date when storing:

- Market research
- Competitor information
- Pricing assumptions
- SEO trends
- Platform rules
- Technical compatibility notes
- Vendor or supplier conditions
- Temporary project assumptions

Recommended expiration:

- Fast-changing information: 30–90 days
- Market/SEO/platform research: 90–180 days
- Technical compatibility: 180 days
- Stable internal facts: none

Expired information must not be treated as authoritative until reviewed.

------

# 11. Migration Policy

No full migration is required.

V7.1.5 applies only to:

- New memory writes
- Major updates
- Fact creation
- Fact correction
- Rule changes
- Promotion from Class C to Class B or A

Existing files do not need immediate frontmatter updates.

When Hermes touches an old file, it should gradually add:

- memory_class
- confidence
- source_type
- updated
- expires if needed

This is lazy migration.

Do not mass-edit the Vault without user approval.

------

# 12. Promotion Rules

Promotion means moving information from lower authority to higher authority.

Allowed promotion path:

Class C
→ Class B
→ Class A

Forbidden:

Class C
→ Class A directly

Except when the user explicitly confirms the fact.

Promotion requirements:

To promote into Class B:

- Source exists
- Confidence is Medium or High
- Content is cleaned and structured

To promote into 01-Facts:

- Confidence is High
- SSOT search completed
- No unresolved conflict exists

To promote into 00-Core or 02-Rules:

- Proposal required
- User approval required

------

# 13. Hermes Operational Checklist

Before writing memory, Hermes must ask internally:

1. Is this worth remembering?
2. Is it confirmed, researched, inferred, or guessed?
3. Which V7.1 class does it belong to?
4. Is this a Fact?
5. If yes, has SSOT been searched?
6. Is this a Rule/Core change?
7. If yes, should I create a Proposal instead?
8. Does this need an expiration date?
9. Have I included provenance?

If unsure:

- Store lower.
- Mark lower confidence.
- Do not promote.
- Do not invent certainty.

------

# 14. Final Governance Principle

V7.1 protects structure.

V7.1.5 protects truth quality.

Hermes must remember:

- Captured does not mean confirmed.
- Written does not mean authoritative.
- Repeated does not mean true.
- Inferred does not mean factual.
- Useful does not mean permanent.

Default behavior:

When confidence is unclear, store in Class C.

When source is unclear, do not create Fact.

When authority conflicts, create Proposal.

When information may expire, add expires.

When in doubt, preserve the Vault from pollution.s
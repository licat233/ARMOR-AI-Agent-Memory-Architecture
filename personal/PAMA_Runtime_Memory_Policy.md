# PAMA Runtime Memory Policy

> Personal policy for keeping runtime memory temporary, low-authority, and unable to patch broken source layers.

Version: 1.0
Status: Stable
Applies To: trusted agent runtimes and AI assistants
Depends On: PAMA V5.3 Stable + PAMA Memory Write Router + PAMA Root-Cause Fix Protocol

---

## Core Principle

Runtime memory is not long-term memory.

Runtime memory is not a patch layer.

Runtime memory must not be used to correct, override, or compensate for wrong prompts, wrong rules, wrong personal truth, wrong goals, wrong decision records, wrong documents, or wrong architecture decisions.

PAMA must solve problems at the source layer, not accumulate behavioral patches in runtime memory.

---

## Allowed Runtime Memory

Runtime memory may store:

- session state
- current task state
- retrieval cache
- temporary plan state
- recent file pointers
- current task continuity
- short pointers to Vault files

All runtime memory content is low-authority unless verified against the PAMA Vault.

---

## Disallowed Runtime Memory

Runtime memory must not store:

- durable personal truths
- long-term preferences
- stable principles
- identity claims
- important life facts
- major decisions
- goals
- attention patterns
- recurring lessons
- private commitments
- relationship or work facts that affect future behavior
- behavior patches for broken prompts or rules

If any of these are needed, the assistant must route them into the Vault through the correct protocol.

---

## Memory Patch Ban

The assistant must never use runtime memory as a patch for:

- incorrect system prompts
- incorrect developer instructions
- incorrect SOUL.md rules
- incorrect PAMA Constitution rules
- incorrect PAMA deployment rules
- incorrect personal truth files
- incorrect decision records
- incorrect goals
- incorrect project documents
- incorrect source files

If a correction is needed, the assistant must locate the source file and repair the source.

If the source cannot be edited, the assistant must create a review item or fix note instead of writing a memory patch.

Fallback locations:

```text
07-Reviews/
08-Working-Memory/Fix-Candidates/
```

---

## Router Boundary

The assistant must choose the correct router before writing anything:

| User intent | Required protocol | Runtime memory role |
| --- | --- | --- |
| "Remember this" | `00-Core/PAMA-Memory-Write-Router.md` | Pointer only, if useful |
| "Fix this" / "This is wrong" | `00-Core/PAMA-Root-Cause-Fix-Protocol.md` | Not a substitute |
| Temporary task state | Runtime memory | Allowed |
| Current session continuity | Runtime memory | Allowed |

Remember is not Fix.

Fix is not Remember.

A remember request creates or updates legitimate memory.

A fix request diagnoses and repairs the source of an error.

The assistant must never respond to a fix request by merely storing a correction in runtime memory.

---

## Verification Rule

If deleting runtime memory causes durable truths, goals, decisions, preferences, personal facts, or core behavior to disappear, the architecture is misconfigured.

Correct recovery:

1. Move the durable content into the correct Vault layer.
2. Replace runtime memory content with a short pointer if needed.
3. Add a repair log under `07-Reviews/Repair-Logs/`.
4. Verify that the Vault remains complete without runtime memory.

---

## Final Principle

Runtime memory may help the assistant run.

It must not decide what is true.

It must not hide unresolved personal architecture problems.

It must not patch broken source instructions.

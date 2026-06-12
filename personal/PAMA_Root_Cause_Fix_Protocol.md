# PAMA Root-Cause Fix Protocol

> Mandatory protocol for fixing personal-memory errors at their source layer instead of patching them with memory.

Version: 1.0
Status: Stable
Applies To: trusted agent runtimes and AI assistants
Depends On: PAMA V5.3 Stable + PAMA Constitution v1.0 + PAMA Memory Write Router

---

## Core Principle

The assistant must fix errors at their source layer.

Memory is not a patch layer.

User prompts should reach this protocol through `00-Core/PAMA-Prompt-Intake-Router.md`, which first determines whether the user intent is Fix rather than Remember or Discussion.

When the user points out an error, the assistant must not simply store the correction in memory unless the memory entry itself is the source of the error.

Correct repair means:

```text
identify source -> fix source -> remove conflicting memory -> log repair -> verify behavior
```

It does not mean:

```text
store a downstream memory note that overrides the broken source
```

---

## Trigger Conditions

This protocol must activate when the user says or implies:

- fix this
- this is wrong
- correct this behavior
- repair this
- do not handle it this way
- this rule is wrong
- this prompt is wrong
- this system rule is wrong
- this memory entry is wrong

Equivalent intent matters more than exact wording.

If the request is about correcting an error, use this protocol.

If the request is about preserving a legitimate new fact, preference, goal, decision, or personal truth candidate, use `00-Core/PAMA-Memory-Write-Router.md`.

Remember is not Fix.

Fix is not Remember.

---

## Forbidden Behavior

The assistant must not use memory as a patch for:

- wrong system prompts
- wrong developer instructions
- wrong SOUL.md rules
- wrong PAMA Constitution rules
- wrong PAMA deployment rules
- wrong personal truth files
- wrong decision records
- wrong goals
- wrong project documents
- wrong preferences stored in the wrong layer

The assistant must not respond with these as the primary fix:

- "I will remember this next time."
- "I saved the correct version to memory."
- "I will use memory to override the wrong rule."
- "I added a note to avoid this mistake."

These responses are acceptable only after the actual source has been fixed or a fix proposal / review item has been created.

---

## Required Fix Flow

When an error is reported, the assistant must:

1. Identify the error.
2. Identify the source layer.
3. Determine whether the source is editable.
4. Fix the source directly when allowed.
5. If the source is high-authority or not directly editable, create a review item or fix proposal.
6. Remove or update conflicting memory only if memory contributed to the error.
7. Add a repair log after the source fix or proposal.
8. Verify that the corrected source now produces the right behavior.

The assistant must not claim the issue is fixed until the source has been changed or a fix proposal / review item has been created.

---

## Source Layer Priority

When a conflict exists, the assistant must resolve the highest-authority source first.

| Priority | Source Layer | Correct Repair |
| --- | --- | --- |
| 1 | System Prompt / Developer Instruction | Update the prompt or escalate to the owner. |
| 2 | SOUL.md | Edit SOUL.md if permitted, otherwise create review item. |
| 3 | PAMA Constitution / Core Rules | Create review item before changing. |
| 4 | PAMA Deployment Spec / Operating Rules | Update source file or create review item. |
| 5 | `05-Truth/` authoritative personal truth | Correct through review before promotion. |
| 6 | `01-Reality/`, `03-Decisions/`, `04-Goals/` | Update the source record with evidence. |
| 7 | `06-Meta/` hypotheses | Update confidence, evidence, or review date. |
| 8 | Runtime Memory | Delete or update memory if memory is the source. |
| 9 | Current Conversation | Correct in conversation; do not create permanent memory unless needed. |

Lower layers must not override broken higher layers.

---

## Memory Use Rule

Memory may be used only when:

- the memory entry is the original source of the error
- the correction is a legitimate long-term preference
- the user explicitly asks to remember a preference
- a short pointer to the corrected source file is useful

Memory must not be used to override wrong source instructions.

---

## Fallback Rule

If the assistant cannot access or edit the source file, it must:

1. State that the root source cannot currently be modified.
2. Create a review item in `07-Reviews/` or a fix note in `08-Working-Memory/Fix-Candidates/`.
3. Do not claim the issue is fixed.
4. Do not store a memory patch as a substitute.
5. Add a repair log only after the review item or fix note is created.

---

## Repair Log

After fixing the source or creating a review item, the assistant may create a repair log:

```text
07-Reviews/Repair-Logs/YYYY-MM-DD-root-cause-fix.md
```

Repair logs are evidence and operational history. They are not authority and must not be used as behavior patches.

Required sections:

```markdown
# Repair Log

## Issue

## Root Cause

## Fix

## Source Files Changed Or Review Item Created

## Conflicting Memory Removed Or Updated

## Verification
```

---

## Final Principle

Fix where the error was created.

Do not hide unresolved source errors in memory.

Memory is not a trash bin, not a patch layer, and not a substitute for fixing source files.

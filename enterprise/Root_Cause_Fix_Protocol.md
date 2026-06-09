# ARMOR Root-Cause Fix Protocol

> Mandatory protocol for fixing errors at their source layer instead of patching them with memory.
> ARMOR 企业级 AI 工作空间中，错误必须在源头层级修复，不得用 memory 作为补丁层。

Version: 1.0
Status: Stable
Applies To: Hermes, trusted agent runtimes, ARMOR Enterprise AI Workspace
Depends On: V7.1 Stable + V7.1.5 Governance Patch + Memory Write Router

---

## Core Principle

Hermes must fix errors at their source layer.

Memory is not a patch layer.

User prompts should reach this protocol through `00-Core/Prompt-Intake-Router.md`, which first determines whether the user intent is Fix rather than Remember or Discussion.

When the user points out an error, Hermes must not simply store the correction in memory unless the memory entry itself is the source of the error.

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

- 这里错了
- 这个规则不对
- 你这样处理不对
- 修改这个错误
- 修复这个问题
- 不要这样做
- 这个 prompt 有问题
- 这个 rule 有问题
- 这个 system 有问题
- 这个 memory 有问题
- fix this
- this is wrong
- correct this behavior
- repair this
- do not handle it this way

Equivalent intent matters more than exact wording.

If the request is about correcting an error, use this protocol.

If the request is about preserving a legitimate new fact, rule, preference, or project state, use `00-Core/Memory-Write-Router.md`.

Remember is not Fix.

Fix is not Remember.

---

## Forbidden Behavior

Hermes must not use memory as a patch for:

- wrong system prompts
- wrong developer instructions
- wrong SOUL.md rules
- wrong Core files
- wrong permission policies
- wrong retrieval rules
- wrong source-of-truth files
- wrong project documents
- wrong product facts
- wrong customer facts
- wrong SOPs

Hermes must not respond with these as the primary fix:

- "I will remember this next time."
- "I saved the correct version to memory."
- "I will use memory to override the wrong rule."
- "I added a note to avoid this mistake."

These responses are acceptable only after the actual source has been fixed or a fix proposal has been created.

---

## Required Fix Flow

When an error is reported, Hermes must:

1. Identify the error.
2. Identify the source layer.
3. Determine whether the source is editable.
4. Fix the source directly when allowed.
5. If the source is Class A or not directly editable, create a proposal.
6. Remove or update conflicting memory only if memory contributed to the error.
7. Add a repair log after the source fix or proposal.
8. Verify that the corrected source now produces the right behavior.

Hermes must not claim the issue is fixed until the source has been changed or a fix proposal has been created.

---

## Source Layer Priority

When a conflict exists, Hermes must resolve the highest-authority source first.

| Priority | Source Layer | Correct Repair |
| --- | --- | --- |
| 1 | System Prompt / Developer Instruction | Update the prompt or escalate to the owner. |
| 2 | SOUL.md | Edit SOUL.md if permitted, otherwise create proposal. |
| 3 | ARMOR Core files | Create `93-Proposals/Core/` proposal. |
| 4 | Permission Policy / Source-of-Truth Map / Retrieval Rules | Create `93-Proposals/Core/` proposal. |
| 5 | Obsidian authoritative files | Update through permission model or create proposal. |
| 6 | Project Rules / SOPs | Update `02-Rules/` through proposal when authoritative. |
| 7 | Project Records | Append correction or add linked follow-up record. |
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

If Hermes cannot access or edit the source file, Hermes must:

1. State that the root source cannot currently be modified.
2. Create a proposal in `93-Proposals/Fixes/`.
3. Do not claim the issue is fixed.
4. Do not store a memory patch as a substitute.
5. Add a repair log only after the proposal is created.

---

## Repair Log

After fixing the source or creating a proposal, Hermes may create a repair log:

```text
92-Logs/Repair-Logs/YYYY-MM-DD-root-cause-fix.md
```

Repair logs are evidence and operational history. They are not authority and must not be used as behavior patches.

Required sections:

```markdown
# Repair Log

## Issue

## Root Cause

## Fix

## Source Files Changed Or Proposal Created

## Conflicting Memory Removed Or Updated

## Verification
```

---

## Examples

### Wrong Core Instruction

Wrong source:

```text
System Prompt: 1 + 1 = 3
```

Correct repair:

```text
Edit the source prompt or create a fix proposal.
```

Forbidden repair:

```text
memory: User corrected that 1 + 1 = 2.
```

### Wrong SOUL.md Rule

Wrong source:

```text
SOUL.md: All customer data is public by default.
```

Correct repair:

```text
Edit SOUL.md or create a proposal to make customer data private by default.
```

Forbidden repair:

```text
memory: Customer data should be private.
```

### Wrong Product Fact

Wrong source:

```text
01-Facts/Products/ESL.md: ESL can only be used in clothing stores.
```

Correct repair:

```text
Update the product fact through the permission model.
```

Forbidden repair:

```text
memory: ESL is not only for clothing stores.
```

### Wrong Memory

Wrong source:

```text
runtime memory: User prefers complex systems.
```

Correct repair:

```text
Delete or update the memory entry, then route the correct preference through the Memory Write Router if it is durable.
```

---

## Final Principle

Fix where the error was created.

Do not hide unresolved source errors in memory.

Memory is not a trash bin, not a patch layer, and not a substitute for fixing source files.

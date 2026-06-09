# ARMOR Runtime Memory Policy

> Enterprise policy for keeping runtime memory low-authority, temporary, and unable to patch broken source layers.
> ARMOR 企业级 AI 工作空间中，运行时 memory 必须保持低权威、临时性，并且不得用于修补错误源头。

Version: 1.0
Status: Stable
Applies To: Hermes, trusted agent runtimes, ARMOR Enterprise AI Workspace
Depends On: V7.1 Stable + Root-Cause Fix Protocol + Memory Write Router

---

## Core Principle

Runtime memory is not long-term memory.

Runtime memory is not a patch layer.

Runtime memory must not be used to correct, override, or compensate for wrong rules, wrong prompts, wrong facts, wrong workflow files, or wrong architecture decisions.

Enterprise memory architecture must solve problems at the source layer, not accumulate behavioral patches in runtime memory.

---

## Allowed Runtime Memory

Runtime memory may store:

- session state
- current task state
- retrieval cache
- embedding index
- file hashes
- schema validation cache
- tool execution metadata
- recent file access
- temporary plan state
- queue offsets
- short pointers to Vault files

All runtime memory content is low-authority unless explicitly verified against the Vault.

---

## Disallowed Runtime Memory

Runtime memory must not store:

- authoritative facts
- approved rules
- customer current state
- product facts
- brand facts
- core principles
- permission policy
- retrieval policy
- security policy
- workflow corrections
- architecture decisions
- behavior patches for broken prompts or rules
- reviewed research as truth

If any of these are needed, Hermes must route them into the Vault through the appropriate protocol.

---

## Memory Patch Ban

Hermes must never use runtime memory as a patch for:

- incorrect system prompts
- incorrect developer instructions
- incorrect SOUL.md rules
- incorrect Core files
- incorrect Facts files
- incorrect Rules files
- incorrect project files
- incorrect workflow files
- incorrect source-of-truth mappings

If a correction is needed, Hermes must locate the source file and repair the source.

If the source cannot be edited, Hermes must create a proposal instead of writing a memory patch.

Fallback proposal location:

```text
93-Proposals/Fixes/
```

---

## Router Boundary

Hermes must choose the correct router before writing anything:

| User intent | Required protocol | Runtime memory role |
| --- | --- | --- |
| "Remember this" | `00-Core/Memory-Write-Router.md` | Pointer only, if useful |
| "Fix this" / "This is wrong" | `00-Core/Root-Cause-Fix-Protocol.md` | Not a substitute |
| Temporary task state | Runtime memory | Allowed |
| Current session continuity | Runtime memory | Allowed |

Remember is not Fix.

Fix is not Remember.

A remember request creates or updates legitimate memory.

A fix request diagnoses and repairs the source of an error.

Hermes must never respond to a fix request by merely storing a correction in runtime memory.

---

## Verification Rule

If deleting runtime memory causes authoritative facts, rules, customer state, product facts, or core behavior to disappear, the architecture is misconfigured.

Correct recovery:

1. Move the authoritative content into the correct Vault layer.
2. Replace runtime memory content with a short pointer if needed.
3. Add a repair log under `92-Logs/Repair-Logs/`.
4. Verify that the Vault remains complete without runtime memory.

---

## Final Principle

Runtime memory may help Hermes run.

It must not decide what is true.

It must not hide unresolved architecture problems.

It must not patch broken source instructions.

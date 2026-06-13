# Changelog

All notable changes to AI Agent Memory Architecture are recorded here.

This project uses project-level semantic versions for repository releases. Architecture branch names such as ARMOR Enterprise V7.2 Stable and PAMA Personal V5.3 Stable may remain unchanged across patch releases when the update adds templates, guides, or maintenance documentation without changing the stable architecture boundary.

## [v1.2.4] - 2026-06-13

### Added

- Added PAMA Personal Execution Workflow as an optional low-authority execution convention for complex personal tasks, goals, and reviews.
- Added PAMA personal execution templates:
  - `task_plan.md`
  - `findings.md`
  - `progress.md`
  - `closeout.md`
- Added Agent Personal Execution Prompt with copy-ready snippets for Codex, Hermes, Claude Code, and other trusted runtimes.
- Added install and update instructions for copying PAMA execution templates into `08-Working-Memory/Templates/Personal-Execution/`.
- Added README and PAMA README entries for the new personal execution workflow and agent prompt guide.

### Changed

- Bumped project version from `v1.2.3` to `v1.2.4`.
- Updated architecture overview diagrams to show AI Agent Memory Architecture `v1.2.4`.
- Kept ARMOR Enterprise at `V7.2 Stable` and PAMA Personal at `V5.3 Stable`; this release does not change the stable architecture boundary.

### Governance Notes

- PAMA execution files are explicitly low-authority working materials.
- Findings, progress, plans, and closeouts do not become Reality, Decisions, Goals source of truth, Truth, or Core policy by themselves.
- Candidate long-term personal memory must still go through the PAMA Memory Write Router, Root-Cause Fix Protocol, or review gate.
- This release intentionally does not add hooks, automatic plan injection, stop gates, attestation, runtime-specific recovery automation, or new top-level Vault folders.

## [v1.2.3] - 2026-06-13

### Added

- Added ARMOR Project Execution Workflow as an optional low-authority execution convention for complex project tasks.
- Added project execution templates:
  - `task_plan.md`
  - `findings.md`
  - `progress.md`
  - `closeout.md`
- Added Agent Project Execution Prompt with copy-ready snippets for Codex, Hermes, Claude Code, and other trusted runtimes.
- Added install and update instructions for copying project execution templates into `70-Schemas/Project-Execution/`.
- Added README and enterprise README entries for the new workflow and agent prompt guide.

### Changed

- Bumped project version from `v1.2.2` to `v1.2.3`.
- Updated architecture overview diagrams to show AI Agent Memory Architecture `v1.2.3`.
- Kept ARMOR Enterprise at `V7.2 Stable` and PAMA Personal at `V5.3 Stable`; this release does not change the stable architecture boundary.

### Governance Notes

- Project execution files are explicitly low-authority working materials.
- Findings, progress, plans, and closeouts do not become Facts, Rules, or Core policy by themselves.
- Candidate long-term memory must still go through the Memory Write Router, Root-Cause Fix Protocol, or proposal workflow.
- This release intentionally does not add hooks, automatic plan injection, stop gates, attestation, runtime-specific recovery automation, or new top-level Vault folders.

## [v1.2.2] - 2026-06-12

### Changed

- Bumped project version to `v1.2.2`.
- Added the architecture overview for agents.
- Kept ARMOR Enterprise V7.2 Stable and PAMA Personal V5.3 Stable as the active architecture branches.

## [v1.2.1] - 2026-06-12

### Added

- Added the agent update guide for aligning existing Vaults with the latest architecture while preserving user content and history.
- Split architecture overview diagrams into separate assets.

### Changed

- Bumped project version to `v1.2.1`.

## [v1.2.0] - 2026-06-12

### Added

- Added PAMA multi-agent shared vault governance.
- Added multi-agent shared vault governance for trusted runtimes sharing one governed Vault.

### Changed

- Tightened runtime adaptation guidance for shared Vault deployments.
- Bumped project version to `v1.2.0`.

## [v1.1.0] - 2026-06-12

### Added

- Released PAMA V5.2 Stable.
- Added Codex ARMOR runtime integration guidance.

### Changed

- Bumped project version to `v1.1.0`.

## [v1.0.0] - 2026-06-11

### Added

- Added architecture visuals to READMEs.
- Added architecture overview diagram.
- Added agent installation guide.
- Established the initial public project release for AI Agent Memory Architecture.

### Changed

- Simplified default enterprise installation.
- Generalized enterprise runtime support.
- Removed legacy Claudian runtime support from the active architecture.

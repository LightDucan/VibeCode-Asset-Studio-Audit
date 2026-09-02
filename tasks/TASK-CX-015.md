# TASK-CX-015 — Production Run Orchestrator & Character Action Pack

STATUS: READY_FOR_QA

Task: TASK-CX-015
Branch: `codex/task-cx-015-production-orchestrator`
BASE: `d216b32d8a6806b4e3843e65e7e7320475437c69`
Implementation Commit: `ef57aedcd22658e1a407a147096c64aadd832d35`

## Scope

Implemented a persisted Character Production Manifest and deterministic orchestration contract over the accepted Motion, VFX source-curation, VFX overlay, asset-library, variant, preview, and export stages. Actions are generic/customizable, required and optional requirements are represented, and manifests reference existing runs/assets rather than copying frames.

`plan()` is a write-free dry run. `run_ready()` and `run_to_next_review()` advance only deterministic stages and stop at human gates. `resume()` continues from persisted checkpoints after approval without rerunning accepted upstream work. The orchestrator records stage transitions, supports stale propagation/minimal rebuild boundaries, action isolation, exact asset references, local lock recovery, owned-root path validation, and failure-safe state preservation.

`action_pack.json` is generated only when required actions are complete. A lightweight production dashboard exposes Run Ready, review, timing, VFX, preview, and export controls. Public evidence includes two actions, a motion-only action, shared Base Motion references, two VFX variants, stale-isolation, resume/checkpoint, path-safety, and source-immutability summaries.

Milestone: REUSABLE BASE MOTION + VERSIONED VFX ASSET + ACTION VARIANT BINDING (project remains open; CX-016 is not started).

Tests: 140 passed, 0 failed.

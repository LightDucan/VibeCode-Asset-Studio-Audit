# TASK-CX-012 — VFX Overlay Core MVP

STATUS: READY_FOR_QA

Task: TASK-CX-012
Branch: `codex/task-cx-012-vfx-overlay-core`
BASE: `c1ef6e8f72bf774917d8222129e0ab8bab2373c2`
Implementation Commit: `8eafc577bd5e26c91dcccfc03eeacee928db53f2`

## Scope

Implemented a separate, run-scoped VFX overlay layer. Ordered VFX PNG frames are converted from black backgrounds to deterministic RGBA, optionally cleaned through explicit normalized regions, and composited against immutable Step 10 motion preview frames.

The MVP supports local-space metadata, manual/keyframed anchors with linear interpolation, translation, rotation, uniform scale, flips, independent timing selection, NORMAL_ALPHA and ADDITIVE blending, behind/front layer ordering, overflow warnings, stale checks, atomic staging promotion, and a lightweight CHARACTER/VFX/COMPOSITE workspace.

The motion pipeline remains reusable and immutable; VFX outputs are derived assets only. The deterministic fixture includes alpha and composite manifests plus a composite PNG with SHA-256 evidence.

Milestone: MOTION PIPELINE MVP COMPLETE (project remains open; CX-013 is not started).

Tests: 120 passed, 0 failed.

# TASK-CX-008 — Canvas + Alignment

STATUS: READY_FOR_QA
BASE: `287d5ec8f0c1024cb0c25707593347c81c9ed1a1`
Branch: `codex/task-cx-008-canvas-alignment`
Implementation Commit: `96b187237e25569468ab132c887489c11598a7d1`

Implemented Pipeline Step 08 `canvas_alignment` with one deterministic
sequence-level scale, robust ground/contact anchors, reference-frame drift
estimation, motion-preserving translations, transparent fixed-canvas output,
premultiplied-alpha resampling, overflow/outlier/confidence warnings, stale
detection, atomic promotion, and an immutable Step-07 input contract. The
alignment workspace provides before/aligned/reference comparison and overlay
controls. Ordered PTS/duration metadata is exposed unchanged for Step 09; no
timing behavior is implemented.

Tests: 98 tests passed, 0 failed.

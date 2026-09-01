# TASK-CX-009 — Animation Timing

STATUS: READY_FOR_QA
BASE: `96b187237e25569468ab132c887489c11598a7d1`
Branch: `codex/task-cx-009-animation-timing`
Implementation Commit: `645dd0e17a12fffec117d81c7f152bca2f13940a`

Implemented metadata-only Pipeline Step 09 `animation_timing`. Canonical fixed-FPS
timing uses integer `hold_ticks` and rational `fps_num/fps_den`; SOURCE_TIMING
preserves source PTS/duration semantics. The service supports 12/15/18/24 FPS,
per-frame and batch holds, notes, preset switching, undo/redo, advisory warnings,
stale-input protection, atomic persistence, deterministic playback values, and
the Step-10 handoff contract. The timing workspace provides timeline controls,
keyboard references, loop/play-once rhythm preview, and statistics. No PNG is
modified, duplicated, deleted, reordered, blended, or interpolated.

Tests: 104 tests passed, 0 failed.

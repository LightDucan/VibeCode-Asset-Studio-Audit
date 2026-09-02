# TASK-CX-013 — VFX Source Intake, Review & Curation

STATUS: READY_FOR_QA

Task: TASK-CX-013
Branch: `codex/task-cx-013-vfx-source-curation`
BASE: `d4c4b22058a9e18709ba3284f9d0d4e388a8e769`
Implementation Commit: `f73b03b7d3f27cc020f1861f4dcdf8e536c055f5`

## Scope

Implemented a run-scoped VFX source workflow for VIDEO and PNG_SEQUENCE input. Intake records immutable source identity and media metadata, validates trim ranges, and supports MP4/MOV/WEBM through the existing probe/decoder infrastructure. Extraction preserves source frame index, timestamps, PTS, durations, and lossless PNG masters using staging promotion.

Review supports KEEP/DROP, toggles, range selection, clear/select-all, manual quality flags, informational phase tags, and a deterministic source-frame review workspace. Curation preserves canonical temporal order, references extracted master PNGs without copying them, and exposes `ordered_vfx_frames[]` directly consumable by CX-012.

The existing CX-012 black-to-alpha, anchor, timing, and composite engine remains the owner of downstream VFX processing; no motion assets are modified.

Milestone: BASIC MOTION + VFX + TIMING (project remains open; CX-014 is not started).

Tests: 128 passed, 0 failed.

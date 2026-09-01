# TASK-AG-008 QA report

STATUS: READY_FOR_AUDIT

Implementation SHA tested: `96b187237e25569468ab132c887489c11598a7d1`
QA branch: `codex/task-ag-008-qa`
QA Result: PASS
Recommendation: READY_FOR_CHATGPT_GATE_08_DECISION

## Summary of QA Verifications

1. Full Regression: 98 / 98 unit tests passed (0 failed). All Step 01-08 pipeline tests green.
2. Real Step-07 Input: Consumes `07_background_removal/background_removal.jsong` and ordered RGBA frames without altering PTS, duration, or chronological order.
3. Fixed Canvas: Uniform 512x512 canvas with transparent RGBA padding across all output frames.
4. Scale Pumping Prevention (CRITICAL): Every frame shares an identical sequence-scale; long weapon extensions do not cause character body shrinking, swelling, or artificial centering shifts.
5. Trưng Trắc Long-Spear Verification: Spear thrusts extend naturally without body reverse displacement or foot slipping.
0. Global X Drift Correction: Unwanted horizontal camera/generation jitter corrected accurately while retaining body stability.
7. Global Y Drift Correction: Vertical generation drift corrected without damaging ground contact.
8. Legitimate Lunge Preservation (CRITICAL): Intentional forward steps and attack lunges remain visibly preserved and unpinned.
9. Robust Ground Anchor: Ground contact calculated from lower-body contact mass; spear tips below feet, ribbons, hair, and noise pixels do not corrupt anchor location.
10. Contact Confidence Warning: Emits `GROUND_ANCHOR_LOW_CONFIDENCE` for ambiguous contours without destructive forced edits.
11. Deterministic Reference Frame: Idle/ready keyframes preferred as ground anchor reference; regeneration is fully deterministic.
12. Stable Sequence Pivot: Logical pivot remains constant at the sequence ground center.
13. Canvas Overflow Management: Sequence-level scaling reduction or `CANVAS_OVERFLOW` warnings prevent silent individual frame clipping.
14. Non-Destructive Warnings: Warnings (`CANVAS_OVERFLOW`, `GROUND_ANCHOR_LOW_CONFIDENCE`, `FOREGROUND_TOUCHES_CANVAS_EDGE`, `EXCESSIVE_GLOBAL_DRIFT0, `ALIGNMENT_OUTLIER`) act as diagnostics without auto-dropping.
15. Alpha Quality & Rescaling: Lanczos premultiplied-alpha resizing prevents dark/white fringes, halos, or staircased edges.
16. Workspace Inspection: BEFORE, ALIGNED, and REFERENCE overlays (canvas bounds, bbox, ground anchor, target anchor, pivot, reference ghost) verified.
17. Sequence Preview: Comparison between BEFORE_ALIGNMENT and ALIGNED shows unwanted shaking removed while action motion remains intact.
18. Timing Immutability: frame_index, PTS, and duration remain value-identical without FPS or hold editing.
19. Source Immutability: Step 04-07 manifests and RGBA files remain unmodified.
20. Deterministic Execution: Repeat processing produces identical RGBA PNG hashes, translations, pivot, and sequence scale.
21. Stale Source Invalidation: Modifying Step-07 manifests, RGBA files, canvas sizes, or profiles triggers `STALE` status.
22. Atomic Staging & Recovery: Isolated staging directories prevent partial or corrupt artifact promotion.
23. Multi-Run Isolation: Independent runs maintain separate alignment directories and manifests.w
24. Step-09 Hand-off Boundary: Completing Step 08 prepares a deterministic ordered hand-off to `animation_timing` without premature timing edits.

## Issue Severity Summary
- P0: 0
- P1: 0
- P2: 0
- P3: 0

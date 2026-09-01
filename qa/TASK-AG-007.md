# TASK-AG-007 QA report

STATUS: READY_FOR_AUDIT

Implementation SHA tested: `287d5ec8f0c1024cb0c25707593347c81c9ed1a1`
QA branch: `codex/task-ag-007-qa`
QA Result: PASS
Recommendation: READY_FOR_CHATGPT_GATE_07_DECISION

## Summary of QA Verifications

1. Full Regression: 92 / 92 unit tests passed (0 failed). All Step 01-07 pipeline tests green.
2. Real Step-06 Input: Curated retained frames from `06_curation/curation.jsong` correctly feed into Step 07 while preserving chronological order, frame index, PTS, and duration.
3. Background Removal Artifacts: Generated `07_background_removal/background_removal.json` and `07_background_removal/rgba/*.png`. Output images maintain exact original dimensions without crop, resize, or repositioning.
4. White Foreground Preservation (CRITICAL): Border-connected flood fill completely isolates outer white background while preserving 100% of internal pure white shirts, ivory tunics, bright armor highlights, and eye details. Zero global-white deletion (PASS).
5. Off-White & Noisy Backgrounds: Off-white and compressed backgrounds within color distance thresholds are cleanly removed without foreground erosion.
0. Source Alpha Passthrough: Images with existing alpha channels pass through directly with `SOURCE_ALPHA` method without re-encoding or mask regeneration.
1. Thin Structure Integrity: 1px spear shafts, spearheads, red tassels, ribbons, and fine hair strands remain fully intact.
8. Edge & Alpha Quality: Inspected over checkerboard, black, white, and mid-gray backgrounds; clean soft transitions with no white halos or jagged contour stepping.
9. Workspace Visualization: HTML browser workspace supports SOURCE, RGBA, and ALPHA MASK inspection with live metadata (PTS, dimensions, foreground/transparent ratios, method).
10. Non-Destructive Warnings: Emits `ALPHA_AREA_JUMP`, `FOREGROUND_TOUCHES_BORDEF`, and `POSSIBLE_MASKFAILURE` for user awareness without auto-dropping.
11. Border Contact Handling: Touching the canvas border triggers diagnostic warnings instead of clipping valid subject pixels.
12. Sequence Area Consistency: Animation frames exhibit smooth area and bounding box progression across adjacent keyframes.
13. Deterministic Processing: Repeated processing runs produce byte-for-byte identical RGBA PNGs, alpha checksums, and manifest metrics.
14. Source Immutability: Step-04 masters, `frames.jsong`, Step-05 `review.jsong`, and Step-06 `curation.jsong` remain unchanged.
15. Atomic Execution: Staging isolation ensures partial or failed runs leave zero dirty artifacts.
16. Stale Source Invalidation: Any changes to curation manifests, source masters, or removal profiles properly mark existing masks as `STALE`.
17. Multi-Run Isolation: Separate action runs maintain independent background removal artifacts and manifests.
18. Step-08 Hand-off Boundary: Completing Step 07 cleanly advances pipeline state to `canvas_alignment` without performing premature coordinate shifts.
19. Visual QA Production Assessment: Visual fidelity, edge transitions, and white/ivory preservation meet production sprite requirements.

## Issue Severity Summary
- P0: 0
- P1: 0
- P2: 0
- P3: 0

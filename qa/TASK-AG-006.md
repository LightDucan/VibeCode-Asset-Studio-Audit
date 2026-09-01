# TASK-AG-006 QA report

STATUS: READY_FOR_AUDIT

Implementation SHA tested: `2f9b46edec60aba46c6e2678927e44bd5d724a73`
QA branch: `codex/task-ag-006-qa`
QA Result: PASS
Recommendation: READY_FOR_CHATGPT_GATE_06_DECISION

## Summary of QA Verifications

1. Full Regression: 84 / 84 unit tests passed (0 failed). All Step 01-06 pipeline tests green.
2. Golden Shoot Input: Step-05 DROP frames are excluded from curation candidates; KEEP frames are active candidates; KEY frames are candidates with active protection.
3. Curation Manifest: Real `06_curation/curation.json` artifact generated and verified locally, linking `source_frames_manifest` and `source_review_manifest` with verified source checksums.
4. Duplicate Assistance: `EXACT_DUPLICATE`, `NEAR_DUPLICATE`, and `STATIC_HOLD` heuristics flag frames without auto-dropping.
5. Blur Detection: Raw Laplacian variance blur score calculated; `POSSIBLE_BLUR` acts as a non-destructive visual suggestion.
6. Suspicious Change: `SUSPICIOUS_CHANGE` heuristic flags large temporal distance jumps without asserting speculative AI anatomy claims.
7. KEY Protection: KEY frames reject heuristic, single manual, and batch DROP attempts unless an explicit override flag and non-empty reason are supplied.
8. Similarity Groups: Stable group IDs (e.g. `static_hold-001`), accurate member indexing, and representative candidate selection without cascading drops.
9. Side-by-Side Workspace: Displays master current and master representative with frame index, PTS, decision, flags, blur score, and distance metadata.
10. Filter Navigation: Verified ALL, FLAGGED, DUPLICATES, BLUR, SUSPICIOUS, and CURATED_KEEP filters.
11. Manual Curation & History: KEEP, DROP, IGNORE, Clear, batch operations, undo, and redo operate with isolated state transitions.
12. Timing-Safe Preview: PRE_CURATION and CURETED_ONLY modes preserve chronological Step-04 order and native PTS durations without synthetic duplicate injection or hold distortion.
13. Source Immutability: Step-04 master PNGs, `frames.json`, PTS values, and Step-05 `review.json` remain untouched.
14. Persistence Across Reopen: Curation manifest, groups, decisions, and progress counters reload accurately without re-running Step 04 or 05.
15. Stale Source Detection: Modifying source frames or review manifests triggers `STALE` status requiring explicit re-analysis.
16. Multi-Run Isolation: Multi-run tests confirm separate state persistence without cross-run artifact bleeding.
17. Step-07 Hand-off: Completing curation exposes deterministic ordered retained-frame references to `background_removal` referencing original Step-04 masters.
18. Visual & Workflow QA: Assistant ergonomics clearly present heuristics as advisory suggestions while keeping the user in full control.

## Issue Severity Summary
- P0: 0
- P1: 0
- P2: 0
- P3: 0

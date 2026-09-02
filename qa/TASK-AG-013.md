# TASK-AG-013 QA report

STATUS: READY_FOR_AUDIT

Implementation SHA tested: `d776e71f930cc9f174cb51fb9daf093a4d7ff46e`
QA branch: `codex/task-ag-013-qa`
QA Result: PASS
Recommendation: READY_FOR_CHATGPT_GATE_13_DECISION

## Summary of QA Verifications

1. Full Regression: 128 / 128 unit tests passed (0 failed). All Step 01-13 pipeline tests green.
2. Real Video Intake: Tested video probe metadata (dimensions, fps, duration, frame_count, codec) and immutability of raw video source.
3. Format Support: Validated MP4, MOV, WEBM support; unsupported formats fail-closed with `VFX_INTAKE_UNSUPPORTED_FORMAT`.
4. Probe Failure Handling: Rejects missing/corrupted files with `VFX_INTAKE_SOURCE_MISSING` and `VFX_INTAKE_PROBE_FAILED`.
5. Trim Range: Validated source-relative sub-second trim ranges without altering source files; invalid ranges raise `VFX_INVALID_TRIM_RANGE`.
6. Multi-Frame Extraction Proof (REQUIRED): Real 3-frame deterministic QA fixture created and verified (`frame_000001.png`, `frame_000002.png`, `frame_000003.png`) with 3 distinct SHA256 checksums (`5637faa309...`, `a41ffd0e79...`, `9af78d3e97...`).
7. Source Frame Identity: Preserves `source_frame_index`, `source_timestamp`, `source_pts`, `source_duration`, and PNG SHA256 accurately.
8. Deterministic Extraction: Repeated extraction from identical inputs produces byte-identical PNG frames and manifests.
9. Lossless Master Extraction: Frames extracted losslessly without premature black-to-alpha or downscaling.
10. Review Workspace UI: Verified KEEP, DROP, toggle, range selection, and selection counters.
11. Review Flags: Manual flags (`BLUR`, `MORPH`, `ARTIFACT`, `DUPLICATE`, `BAD_SHAPE`, `BAD_DIRECTION`) remain strictly informational without automated frame deletion.
12. Phase Tags: `CHARGE`, `RELEASE`, `PEAK`, `IMPACT`, `DISSIPATE` persist as review metadata without altering sequence order.
13. Non-Contiguous Curation: Verified selecting non-contiguous source frames (e.g. 1, 2, 3) assigns contiguous sequence indices (1, 2, 3) while preserving original source frame indices and temporal ordering.
14. Zero Duplicate Physical Copies: Curation manifest references extracted master PNGs directly without duplicating files on disk.
15. Zero Selection Rejection: Saving curation with zero selected frames raises `VFX_NO_SELECTION`.
16. PNG Sequence Intake: Validated multi-frame PNG sequence ingestion with consistent dimension verification and natural sorting.
17. Long-Tail Workflow: Cleanly trims and drops irrelevant late particle tails while preserving the core effect.
18. Direct CX-012 Handoff (CRITICAL): `curation.json` feeds directly into `VFXOverlayService.process_alpha` and `composite_sequence` without manual manifest rewriting or path modifications.
19. CX-012 Non-Regression: Verified all Step-12 overlay, anchor interpolation, transform, and composite contracts remain green.
20. Stale State Detection: Any modifications to intake sources, trim ranges, or extracted frame checksums flag downstream states `VFX_CURATION_STALE`.
21. Downstream Stale Propagation: Modifying curation frames invalidates downstream CX-012 overlays and composites.
22. Source Immutability: Raw video/PNG sources and character motion assets remain 100% untouched.
23. Atomic Staging: Staging directories (`.vfx-extract.*.staging`) ensure zero partial artifacts on failure.
24. Multi-Run Isolation: Directional_A, TripleLine_B, Crescent_C runs maintain completely isolated intake, extraction, and curation manifests.
25. Playback Clock Consistency: Source review follows Step-10 clock-anchored playback design without float drift.
26. Workspace Flow: Complete end-to-end user path (Intake -> Probe -> Trim -> Extract -> Review -> Curate -> Send to VFX Overlay) verified.
27. Scope Control: Strict adherence to source intake, extraction, review, and curation; no AI generation, spritesheet baking, or exporter creep.

## Issue Severity Summary
- P0: 0
- P1: 0
- P2: 0
- P3: 0

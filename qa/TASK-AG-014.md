# TASK-AG-014 QA report

STATUS: READY_FOR_AUDIT

Base commit: `d776e71f930cc9f174cb51fb9daf093a4d7ff46e`
Implementation SHA tested: `d216b32d8a6806b4e3843e65e7e7320475437c69`
QA branch: `codex/task-ag-014-qa`
QA Result: PASS
Recommendation: READY_FOR_CHATGPT_GATE_14_DECISION

## Summary of QA Verifications

1. Full Regression: 133 / 133 unit tests passed (0 failed). Complete Step 01-14 test suite green.
2. Real Content Checksums (GATE BLOCKER): Replaced sentinel placeholders (`aaaa...`, `bbbb...`, `eeee...`, `1111...`, `2222...`) with real computed SHA256 checksums across all assets, variants, and composites.
3. Content Checksum Reproducibility: Independently recomputed content checksums from canonical inputs (`curation_checksum`, `alpha_checksum`, `cleanup_profile`, `black_to_alpha_profile`, `local_space`, and metadata). Verified exact reproducibility across repeated runs.
4. Checksum Sensitivity: Verified that changes to curation checksum, alpha checksum, cleanup profile, black-to-alpha profile, local origin, or forward direction change the content checksum; while timestamps, machine paths, and UI preferences do not affect canonical identity.
5. Real Registered Asset: Registered real deterministic QA VFX asset (`directional-slash-v1`, version `1.0`) with 3 distinct frames, local origin `(0, 0)`, forward direction `(1, 0)`, and real content checksum `a0596d7bc4fc1e64cb4b92c2a197a3886f5d479189ea325c90473a5c21d02ae0`.
6. Second Distinct Asset: Registered second distinct VFX asset (`radial-burst-v1`, version `1.0`) with 3 distinct frames and real content checksum `ab661918aef9ede0f16dea7364144922727fb1a64df5e3b834659082fd3b8bae` (`Asset A != Asset B`).
7. Character-Agnostic Asset Contract: Manifests contain no hero IDs, absolute screen positions, character anchor tracks, or skill motion frame numbers.
8. Library Index: Verified index is deterministic, sorted by `(asset_id, version)`, and accurately indexes all assets with metadata and checksums.
9. Exact Version Resolution: Verified resolving `directional-slash-v1` version `1.0` and `2.0` returns the exact requested versions without implicit "latest" substitution.
10. Immutable Version (CRITICAL): Modifying registered asset definition on disk and attempting to re-register version `1.0` is rejected with `VFX_ASSET_VERSION_EXISTS`. Creating version `2.0` leaves `1.0` bytes completely intact.
11. New Version Difference: Version `2.0` with modified local space produces a different content checksum while both versions remain independently resolvable.
12. Real Base Motion Reuse (CRITICAL): Verified `Variant A` and `Variant B` bind to the exact same motion preview (`6b4f210b3815820e95d61f24c5a9c813563cf8cd133490cc8ed27a353134912e`).
13. Two VFX / One Motion (CRITICAL): Verified same motion checksum (`6b4f210b3815...`), distinct VFX content checksums (`a0596d7bc4...` vs `ab661918ae...`), and distinct derived composite checksums (`02fccbef43...` vs `f77959d631...`).
14. Real Composite Proof (REQUIRED): Variants invoke accepted CX-012 compositor. Derived `composite.json`, first composite PNG, and last composite PNG published with real SHA256 hashes. Active VFX frames satisfy `motion PNG SHA != composite PNG SHA`.
15. No Fake Composite Checksum: Recomputed composite manifest SHA256 matches `variant.json` `output.composite_checksum` exactly (`02fccbef43...` and `f77959d631...`).
16. Same VFX / Two Motions: Reusable VFX assets can be bound to separate motions with separate anchor tracks/transforms without source duplication.
17. Zero Duplication (CRITICAL): Creating 10 action variants generates reference metadata only, with 0 duplicated physical copies of motion PNGs, curated VFX PNGs, or alpha VFX PNGs.
18. Source File Count Proof: Source motion PNGs (3 files), curated VFX PNGs (3 files), and alpha VFX PNGs (3 files) retain identical file counts and SHA256 hashes before and after 10 variants.
19. Override Resolution: Asset defaults (`scale=1.0`, `rotation=0`, `blend=NORMAL_ALPHA`, `layer=FRONT_OF_CHARACTER`) cleanly overridden by variant configurations (`scale=0.8`, `rotation=15.0`, `blend=ADDITIVE`) without mutating the asset manifest.
20. Anchor Track Isolation: Anchor tracks (`WEAPON_TIP`, `CHARACTER_CENTER`) exist purely in variant binding metadata.
21. Timing Overrides: Start ticks and time scales are resolved at composite time without mutating base assets.
22. Blend / Layer Overrides: `NORMAL_ALPHA`, `ADDITIVE`, `FRONT_OF_CHARACTER`, and `BEHIND_CHARACTER` composite modes verified.
23. CX-012 Compositor Reuse (CRITICAL): `VFXActionVariantService.compose_variant` calls the accepted `VFXOverlayService.composite_sequence` without duplicate compositing code.
24. Variant State Machine: Verified `DRAFT` -> `READY` -> `STALE` lifecycle states.
25. Stale Motion Detection: Modifying Base Motion frames flags downstream variants `STALE`.
26. Stale VFX Asset Detection: Mismatched/corrupted VFX asset checksums flag downstream variants `STALE`.
27. No Auto-Upgrade on v2: Creating Asset v2 leaves existing Variant bindings targeting v1 unchanged.
28. Determinism: Identical variant configurations produce identical resolved configs, variant JSON payloads, composite PNG bytes, and composite checksums.
29. Library Workspace: Verified HTML editor shell for listing, filtering, selecting, registering, and binding VFX assets.
30. Action Variant Workspace: Verified HTML editor shell for motion selection, VFX binding, transform, timing, blend, layer, and playback controls.
31. Quick Variant Comparison: Switching between variants sharing Base Motion preserves motion source while updating bindings and composites.
32. Source Immutability: Steps 01-11 motion assets, CX-013 curation sources, and CX-012 alpha assets remain 100% untouched.
33. Multi-Run / Multi-Character Isolation: Shared library enables cross-character reuse while isolating variant bindings and composites.
34. Public Audit Evidence: Published real deterministic QA fixtures, manifests, and snapshots.

## Issue Severity Summary
- P0: 0
- P1: 0
- P2: 0
- P3: 0

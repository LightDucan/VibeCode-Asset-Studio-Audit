# TASK-AG-015 QA report

STATUS: READY_FOR_AUDIT

Base commit: `d216b32d8a6806b4e3843e65e7e7320475437c69`
Implementation SHA tested: `78ee4a400b786ad6ce93d8b0dd0899bffecc383c`
QA branch: `codex/task-ag-015-qa`
QA Result: PASS
Recommendation: READY_FOR_CHATGPT_GATE_15_DECISION

## Summary of QA Verifications

1. Full Regression: 140 / 140 unit tests passed (0 failed). Complete Step 01-15 test suite green.
2. Static Destructive-Op Audit (GATE BLOCKER): Confirmed zero occurrences of dangerous recursive deletion (`rm -rf`, `shutil.rmtree`, `os.remove` on arbitrary paths), disk operations, or destructive git operations (`git reset --hard`, `git clean -fdx`, `git checkout --`). All lock management is strictly confined to unlinking `.orchestrator.lock`.
3. Project Root Containment (CRITICAL): Verified that path resolution via `_owned(...)` strictly confines operations to the project root. Traversal escapes (`../`, `../../`), absolute paths outside project, drive roots, and external locations raise `PRODUCTION_PATH_OUTSIDE_ROOT`.
4. Symlink / Resolved-Path Safety: Verified that symlinks resolving to destinations outside the project root fail closed and raise `PRODUCTION_PATH_OUTSIDE_ROOT`.
5. Dry Run Zero Writes (CRITICAL): Verified `plan()` produces zero file creations, zero deletions, zero modifications, zero lock creation, and zero manifest rewrites. Filesystem tree and SHA256 fingerprints before and after `plan()` are 100% identical.
6. Human Gates: Verified deterministic stopping at human judgment stages (`frame_review`, `frame_curation`, `animation_timing`, `vfx_source_curation`, `vfx_asset_binding`). The orchestrator never auto-approves or auto-keeps human gates.
7. `run_to_next_review`: Verified executing `run_to_next_review()` runs only safe ready stages and stops exactly at the first human gate without executing downstream stages.
8. Review Resume: Verified resuming with explicit stage approvals transitions `NEEDS_REVIEW` to `ACCEPTED` and continues from the next valid stage without rerunning previously accepted upstream stages.
9. Checkpoint Persistence: Verified every stage transition records input identity, output identity, stage states, and reason in `checkpoints` and `audit_trail` on disk, allowing full process state recovery across restarts.
10. Interruption During Write: Verified unpromoted staging outputs do not corrupt accepted artifacts, and manifests never point to partial outputs.
11. Failed Rebuild Preservation (GATE BLOCKER): Verified that when a stage rebuild fails, existing accepted outputs remain byte-identical and recoverable, and failure is isolated as `ERROR`.
12. Safe Promotion: Verified staging is validated prior to promotion, preserving accepted identity until promotion succeeds.
13. No Automatic Cleanup: Verified older outputs superseded by new runs are marked `SUPERSEDED` and are never automatically deleted.
14. Same-Run Concurrent Writer: Verified `_RunLock` with `O_CREAT | O_EXCL` blocks concurrent writes and raises `PRODUCTION_RUN_LOCKED`.
15. Stale Lock Recovery: Verified `recover_stale_lock()` unlinks only the specific owned `.orchestrator.lock` file without deleting unrelated files.
16. Action Isolation (CRITICAL): Modifying `BASIC_ATTACK` marks its downstream pipeline `STALE` while `IDLE` and other sibling actions remain `ACCEPTED` with identical artifact SHAs.
17. Minimal Rebuild: Verified changing `animation_timing` invalidates only preview, export, and composite stages, leaving upstream intake, extraction, review, curation, background removal, and alignment intact.
18. VFX-Only Minimal Rebuild: Verified changing variant transform/timing only invalidates and reruns the composite stage without rerunning motion or VFX extraction.
19. Shared VFX Isolation: Modifying Variant A leaves Variant B and the underlying shared VFX Asset in `READY` state.
20. Exact Version Pinning: Verified Variant manifests pin exact versions (e.g. `1.0`), preventing implicit upgrades when `2.0` is registered.
21. Real Checksum Evidence: Eliminated all placeholder strings (`aaaa...`, `bbbb...`, etc.). All Motion checksums (`8f3ecddc9287...`, `5df7ca6bfecc...`), VFX content checksums (`92eb12593dfd...`, `cbb29b2f8ccd...`), and composite checksums (`39cb9db529c0...`, `5deaf05d36de...`) are real computed SHA256 hashes.
22. Motion-Only Production: Verified character with `IDLE` (Motion-only) and `BASIC_ATTACK` reaches `COMPLETE` state and builds a valid `action_pack.json`.
23. Base Motion + Two Variants: Reused a single `BASIC_ATTACK` Base Motion across two distinct skill variants without sequence duplication.
24. Action Pack Validation: Validates all required actions, motion previews, PNG exports, canvases, pivots, and variants prior to marking `COMPLETE`.
25. Fail-Closed Completion: Unapproved gates, missing required actions, or stale actions block `build_action_pack` with `ACTION_PACK_NOT_READY`.
26. Required / Optional Actions: Required actions (`IDLE`, `BASIC_ATTACK`) are enforced while optional actions (`WALK`, `HURT`) do not block completion when unconfigured.
27. Custom Action: Supported arbitrary action IDs (`DASH_ATTACK`) without hardcoded name restrictions.
28. `next_actions`: Generated deterministic action recommendations based on current pipeline state.
29. Orchestrator Service Reuse: Reuses accepted Step 01-14 services (`ProjectService`, `VFXOverlayService`, `VFXAssetLibraryService`) without duplicating domain logic.
30. Progress Calculation: Accurately calculated from accepted stages only.
31. Corrupted Checkpoint: Handled fail-closed on corrupt or missing manifests.
32. Upstream Hash Mismatch: Detects checksum mismatches and marks dependent stages `STALE`.
33. Source Immutability: Verified input video and upstream accepted artifacts remain byte-identical across runs.
34. Outside Sentinel File Test (CRITICAL): Sentinel files outside the project root (`outside_A.txt`, `outside_B.txt`) remained byte-identical with matching SHA256 hashes before and after all orchestrator operations.
35. Sibling Project Safety: Sibling projects remained untouched with identical directory tree and file hashes.
36. Git Safety: Orchestrator executed zero git mutations or VCS commands.
37. Action Pack References: Verified `action_pack.json` references existing asset manifests without duplicating physical PNG sequences.
38. Determinism: Repeated execution with identical inputs produces identical JSON payloads and checksums.
39. Public QA Evidence: Published real deterministic production fixture, manifests, and verification snapshot.

## Issue Severity Summary
- P0: 0
- P1: 0
- P2: 0
- P3: 0

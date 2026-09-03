# TASK-CX-017: Golden Pilot Timing + VFX Binding Preparation

STATUS: READY_FOR_QA

Base commit: `182debc04d534e2b5038d7e488ac749f27085a66`
Branch: `codex/task-cx-017-golden-timing-vfx-binding`
Implementation Commit: `de39d08059346eac64e74b972fcbcec6554c778f`
Integration Implementation SHA: `de39d08059346eac64e74b972fcbcec6554c778f`

## Phase 0: Gate 16 Acceptance Record

- Gate: 16
- Status: ACCEPTED
- Decision: ACCEPTED
- Implementation: `6b4ecf45a0ede338f7132d69ee9c9b5117388365`
- QA Task Commit: `182debc04d534e2b5038d7e488ac749f27085a66`
- Audit Mirror: `a7a4d50b9d8625cc1ca67ace1af4c35a3b8cf0ec`
- Tests: 156 / 156 PASS

## Pilot candidate

Both locked motion curations (Trưng Trắc 12 frames, Trưng Nhị 11 frames) are represented by editable 18/1 FPS timing manifests with logical `hold_ticks`; no PNG is duplicated. Timestamp normalization documents source frame index, presentation timestamp, PTS, and the authoritative frame-index-plus-SHA identity. Step-10 preview candidates expose play, pause, loop, frame/tick scrub, and hold visualization. Timing remains `NEEDS_REVIEW`.

The accepted 12-frame VFX curations are processed through the CX-012 deterministic black-to-alpha provider and registered as immutable CX-014 version-1 assets. Assets use character-agnostic local origin `(0,0)` and forward `(1,0)`; character coordinates are not stored in `asset.json`.

Trưng Trắc binds `LONG_THUONG_PHA_TRAN` v1 at `WEAPON_TIP`; Trưng Nhị binds `TRIPLE_LINE_PRECISION` v1 at `MUZZLE`. Rotation, scale, flip, and offset remain editable transform candidates. Composite previews were produced with `VFXOverlayService.composite_sequence`; motion-only, VFX-only, binding, and composite decisions remain unapproved.

## Final review state

| Character | Animation Timing | VFX Binding | Composite | Production |
| --- | --- | --- | --- | --- |
| Trưng Trắc | NEEDS_REVIEW | NEEDS_REVIEW | NEEDS_REVIEW | READY_FOR_VISUAL_REVIEW |
| Trưng Nhị | NEEDS_REVIEW | NEEDS_REVIEW | NEEDS_REVIEW | READY_FOR_VISUAL_REVIEW |

All four explicitly installed MP4s and the locked curation manifests were fingerprinted before and after preparation and remained unchanged. The public evidence contains metadata/checksums only; no raw video or frame binaries are published. The same curation/timing/asset/binding inputs produce identical candidate checksums. No timing, VFX placement, anchor, or composite was auto-approved.

## Issue Severity Summary

- P0: 0
- P1: 0
- P2: 0
- P3: 0

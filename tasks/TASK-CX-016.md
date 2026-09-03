# TASK-CX-016: Golden Production Pilot (Trưng Trắc + Trưng Nhị)

STATUS: READY_FOR_QA

Base commit: `78ee4a400b786ad6ce93d8b0dd0899bffecc383c`
Branch: `codex/task-cx-016-golden-production-pilot`
Integration Implementation SHA: `6b4ecf45a0ede338f7132d69ee9c9b5117388365`

## Phase 0: Gate 15 Acceptance Record

- **Gate**: 15
- **Status**: ACCEPTED
- **Decision**: ACCEPTED
- **Implementation**: `78ee4a400b786ad6ce93d8b0dd0899bffecc383c`
- **QA Task Commit**: `bbca5f1c77c989dcaa0951b166deb4bd5e26fef4`
- **Audit Mirror Commit**: `c39da131870105eb9e142f188fb81780f028fa8a`
- **Tests**: 140 / 140 PASS
- **Safety**: `PROJECT_ROOT_CONTAINMENT` = PASS, `FAILED_REBUILD_PRESERVATION` = PASS, `HUMAN_GATE_ENFORCEMENT` = PASS, `NO_DESTRUCTIVE_VCS` = PASS

---

## Executive Summary

TASK-CX-016 executes the first real production onboarding through the accepted Step 01–15 orchestration pipeline for the historical heroines **Trưng Trắc** and **Trưng Nhị**.

This task establishes canonical character profiles, source-map registries, logical asset bindings, human gate review preparation, and fail-closed handling for missing raw inputs—strictly preserving source immutability, zero public asset leakage, and cross-character isolation.

---

## Character Production Summaries

### 1. Trưng Trắc (`trung-trac`)

- **Archetype**: WARRIOR
- **Weapon**: Long spear (`long_spear`)
- **Visual Identity**: Historical Vietnamese / Lạc Việt / Đông Sơn warrior queen
- **Canonical Reference**: `examples/golden-trio/trung-trac/trung-trac-canonical.png`
  - Dimensions: 1086 x 1448 px (RGB)
  - Real SHA256: `279900c86ff590a879abdfec22a1846f2c3d808a95f2204521eee50446646db4`
- **Required Pilot Action**: `BASIC_ATTACK`
- **Basic Motion**:
  - Logical Source Alias: `TIMING_PRIORITY_BASIC_THRUST`
  - Candidate Hint: `TIMING_PRIORITY___The_entire_a.mp4`
  - Motion Source: `production_sources/trung-trac/media/basic_attack/TIMING_PRIORITY___The_entire_a.mp4`
  - Motion SHA256: `e503167926b4f0cb5efc693a35457d56a6e0ad3c116b52474806a7e38fb730cb`
  - Motion Probe: 1280 × 720, 24 fps, 10.01 s, 240 frames
  - Motion Status: `NEEDS_REVIEW` (full extraction prepared; human frame review pending)
- **VFX Binding**:
  - Logical Identity: `LONG_THUONG_PHA_TRAN`
  - Effect Type: `DIRECTIONAL` / `PIERCE`
  - Anchor: `WEAPON_TIP`
  - Status: `NEEDS_REVIEW`
  - VFX Source: `production_sources/trung-trac/media/vfx/1000052536.mp4`
  - VFX Content SHA256: `3916b2fd49e1e3211691d2178fbc6a5c3e684339eba9722d7602ef53ce57d16f`
  - VFX Probe: 1280 × 720, 24 fps, 10.01 s, 240 frames
- **Production State**: `READY_FOR_VISUAL_REVIEW`
- **Next Actions**: `REVIEW_BASIC_ATTACK_FRAMES`, `REVIEW_VFX_CURATION`

### 2. Trưng Nhị (`trung-nhi`)

- **Archetype**: ARCHER
- **Weapon**: Crossbow (`crossbow`)
- **Visual Identity**: Historical Vietnamese / Lạc Việt / Đông Sơn crossbow warrior
- **Canonical Reference**: `examples/golden-trio/trung-nhi/trung-nhi-canonical.png`
  - Dimensions: 1086 x 1448 px (RGB)
  - Real SHA256: `e05af1093d0e6c8cb3cbf5715dd34ec881e6cd8a67804577050287006288c22c`
- **Required Pilot Action**: `BASIC_ATTACK`
- **Basic Motion**:
  - Logical Source Alias: `TRUNG_NHI_BASIC_CROSSBOW`
  - Candidate Hint: `1000052543.mp4`
  - Motion Source: `production_sources/trung-nhi/media/basic_attack/1000052543.mp4`
  - Motion SHA256: `9294017851696c0db7c327e582705170c0be05405a1a50fde36e855f0458509a`
  - Motion Probe: 1280 × 720, 24 fps, 10.01 s, 240 frames
  - Motion Status: `NEEDS_REVIEW` (full extraction prepared; human frame review pending)
- **VFX Binding**:
  - Logical Identity: `TRIPLE_LINE_PRECISION`
  - Effect Type: `DIRECTIONAL` / `BURST`
  - Anchor: `MUZZLE`
  - Status: `NEEDS_REVIEW`
  - VFX Source: `production_sources/trung-nhi/media/vfx/1000052538.mp4`
  - VFX Content SHA256: `33f15289414f9fc42eaad665aeeb996c4ad517d4c818ae6d25d9ae97e17775b7`
  - VFX Probe: 1280 × 720, 24 fps, 10.01 s, 240 frames
- **Production State**: `READY_FOR_VISUAL_REVIEW`
- **Next Actions**: `REVIEW_BASIC_ATTACK_FRAMES`, `REVIEW_VFX_CURATION`

---

## Media Map and Human Review Boundary

The four explicitly provided project-owned media files are mapped by logical identity and verified against their byte SHA256. Both BASIC_ATTACK videos completed Step-03 validation and full Step-04 extraction (240 decoded frames each); Frame Review remains `NEEDS_REVIEW`. Both VFX videos completed intake and bounded extraction for review; VFX Review/Curation remains `NEEDS_REVIEW`. No frame was auto-selected, no VFX was auto-curated, no timing was confirmed, and no anchor/composite was approved.

The next human reviews are `REVIEW_BASIC_ATTACK_FRAMES` and `REVIEW_VFX_CURATION` for each character. Source files remained byte-identical throughout validation and extraction.

---

## Technical & Safety Verifications

1. **Originals Immutable**: Verified byte-identical SHA256 before and after for all canonical references (`trung-trac`, `trung-nhi`, `le-chan`).
2. **Explicit Source Mapping Only**: Zero recursive drive scanning or guessed filesystem traversals. Sources resolved only through the four explicit project-relative media paths.
3. **No Public Asset Leak**: Verified that public snapshots contain zero absolute local filesystem paths, zero binary image bytes, and only sanitized relative metadata.
4. **Real Checksums**: Every checksum in profiles, source maps, and manifests is a computed SHA256. Zero sentinel placeholders (`aaaa...`, `bbbb...`).
5. **Human Gate Enforcement**: Orchestration stops deterministically at human gates (`frame_review`, `frame_curation`, `vfx_source_curation`). Never auto-approves.
6. **Cross-Character Isolation**: Modifying Trưng Trắc leaves Trưng Nhị manifest and artifact hashes completely unchanged, and vice versa.
7. **Interruption Safety**: Simulated staging interruption leaves previously accepted outputs and source files intact.
8. **Regression Suite**: 152 / 152 unit tests passing (0 failures).

## Mapped Pilot State

Both required BASIC_ATTACK sources are now explicitly mapped and checksum-verified. Each Character is `READY_FOR_VISUAL_REVIEW`; motion frame review and VFX review/curation remain independent human gates with `NEEDS_REVIEW` status. No frame, timing, anchor, or composite was auto-approved.

## Issue Severity Summary
- P0: 0
- P1: 0
- P2: 0
- P3: 0

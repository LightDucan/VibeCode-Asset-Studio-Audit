# TASK-CX-016: Golden Production Pilot (Trưng Trắc + Trưng Nhị)

STATUS: READY_FOR_QA

Base commit: `78ee4a400b786ad6ce93d8b0dd0899bffecc383c`
Branch: `codex/task-cx-016-golden-production-pilot`
Integration Implementation SHA: `e2e34a20d267fc4c2ad4e413fc21749934c734f1`

## Phase 0: Gate 15 Acceptance Record

- **Gate**: 15
- **Status**: ACCEPTED
- **Decision**: ACCEPTED
- **Implementation**: `78ee4a400b786ad6ce93d8b0dd0899bffecc383c`
- **QA Task Commit**: `bbca5f1c77c989dcaa0951b166deb4bd5e26fef4`
- **Audit Mirror Commit**: `c39da131870105eb9e142f188fb81780f028fa8a`
- **Tests**: 150 / 150 PASS
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
  - Motion Status: `BLOCKED_ASSET_INPUT` (No guessed disk search; awaiting explicit user input mapping)
  - Motion Advisory: Approx. 10–14 useful frames (`READY`, `ANTICIPATION`, `THRUST`, `PEAK`, `RECOIL`, `RECOVERY`)
- **VFX Binding**:
  - Logical Identity: `LONG_THUONG_PHA_TRAN`
  - Effect Type: `DIRECTIONAL` / `PIERCE`
  - Anchor: `WEAPON_TIP`
  - Status: `NEEDS_REVIEW`
  - VFX Content SHA256: `92eb12593dfdb1d83556622936032086db6ccbf9db459e709b704fcd49df8cb7`
- **Production State**: `BLOCKED_ASSET_INPUT`
- **Next Actions**: `PROVIDE_BASIC_ATTACK_VIDEO`

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
  - Motion Status: `BLOCKED_ASSET_INPUT` (No guessed disk search; awaiting explicit user input mapping)
  - Motion Advisory: Approx. 9–12 useful frames (`READY`, `AIM`, `PRE-FIRE`, `FIRE`, `RECOIL`, `RECOVERY`)
- **VFX Binding**:
  - Logical Identity: `TRIPLE_LINE_PRECISION`
  - Effect Type: `DIRECTIONAL` / `BURST`
  - Anchor: `MUZZLE`
  - Status: `NEEDS_REVIEW`
  - VFX Content SHA256: `cbb29b2f8ccdd373735341eccb26a2e66b1798cf8cecf4c86a76d6f2014c9e95`
- **Production State**: `BLOCKED_ASSET_INPUT`
- **Next Actions**: `PROVIDE_BASIC_ATTACK_VIDEO`

---

## Missing Asset Inputs

- **`TRUNG_TRAC_BASIC_MOTION`**: Source video `TIMING_PRIORITY___The_entire_a.mp4` / `TIMING_PRIORITY_BASIC_THRUST` not mapped. Recorded fail-closed as `BLOCKED_ASSET_INPUT`.
- **`TRUNG_NHI_BASIC_CROSSBOW`**: Source video `1000052543.mp4` / `TRUNG_NHI_BASIC_CROSSBOW` not mapped. Recorded fail-closed as `BLOCKED_ASSET_INPUT`.

---

## Technical & Safety Verifications

1. **Originals Immutable**: Verified byte-identical SHA256 before and after for all canonical references (`trung-trac`, `trung-nhi`, `le-chan`).
2. **Explicit Source Mapping Only**: Zero recursive drive scanning or guessed filesystem traversals. Sources resolved only through explicit `production_sources/**/source-map.json`.
3. **No Public Asset Leak**: Verified that public snapshots contain zero absolute local filesystem paths, zero binary image bytes, and only sanitized relative metadata.
4. **Real Checksums**: Every checksum in profiles, source maps, and manifests is a computed SHA256. Zero sentinel placeholders (`aaaa...`, `bbbb...`).
5. **Human Gate Enforcement**: Orchestration stops deterministically at human gates (`frame_review`, `frame_curation`, `vfx_source_curation`). Never auto-approves.
6. **Cross-Character Isolation**: Modifying Trưng Trắc leaves Trưng Nhị manifest and artifact hashes completely unchanged, and vice versa.
7. **Interruption Safety**: Simulated staging interruption leaves previously accepted outputs and source files intact.
8. **Regression Suite**: 150 / 150 unit tests passing (0 failures).

## Fail-Closed Pilot State

Both required BASIC_ATTACK sources remain unmapped. Each Character therefore stays `BLOCKED_ASSET_INPUT`; the only valid next action is `PROVIDE_BASIC_ATTACK_VIDEO`. Frame review is not advertised until extraction/review artifacts exist. VFX preparation remains independently `NEEDS_REVIEW` with its real content SHA and anchor identity.

## Issue Severity Summary
- P0: 0
- P1: 0
- P2: 0
- P3: 0

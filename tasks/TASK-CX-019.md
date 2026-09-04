# TASK-CX-019 — Dual-Source Action Production Core + Runtime Handoff

STATUS: READY_FOR_AUDIT

Base commit: `be40f6636ed188cf2b04d71886f41a6b51f68437`
Branch: `codex/task-cx-019-dual-source-action-core`
Implementation SHA: `4f966617150d180838076bd9d3030971b7528c17`
Integration Implementation SHA: `4f966617150d180838076bd9d3030971b7528c17`

## Scope

Provider-neutral action production now records an immutable accepted RAW motion source and versioned derived VFX candidates. Candidate imports are copied into project-owned storage, fingerprinted, and never overwrite the raw source or an earlier version. Acceptance and rejection are explicit transitions.

The prompt contract compiles `RAW_BASIC_ATTACK`, `ADD_BASIC_VFX`, and `ADD_ACTIVE_VFX` from shared identity, weapon, motion, camera, background, VFX, negative-rule, and hard-priority blocks. It invokes no Gemini or other provider API.

Runtime resolution supports `RAW`, `BASIC_VFX`, and `ACTIVE_SKILL_VFX`. Only explicitly accepted candidates are selectable; missing, rejected, or candidate variants fall back to RAW. Version selection is exact and never auto-upgraded.

## Verification

- Tests: 181 / 181 PASS (one platform-limited symlink test skipped when Windows symlink creation is unavailable).
- Raw immutability: PASS.
- Variant versioning: PASS.
- Runtime resolution and RAW fallback: PASS.
- Path containment and symlink-escape safety: PASS where platform permits symlink creation.
- Existing CX-018 runtime exporter remains fail-closed with `RUNTIME_MASTER_MISSING` when accepted aligned masters are absent.
- Gate18 state: `BLOCKED_INPUT` / `BLOCKED_MASTER_HANDOFF`; no runtime pack was fabricated.
- Files deleted: NONE.
- HuyenSu-TD writes: NONE.
- P0: 0
- P1: 0
- P2: 0
- P3: 0

### Known limitations

- Gate18 still awaits accepted aligned PNG master sequences before runtime packs can be exported.
- This Python-only repository has no `package.json`; npm commands remain unavailable.

# TASK-CX-018: Runtime Asset Export Pack

STATUS: BLOCKED_INPUT

Base commit: `773256025fe97e489a3dba88e37265b18de4f283`
Branch: `codex/task-cx-018-runtime-export-pack`

## Phase 0: Gate 17 Acceptance Record

- Gate: 17
- Status: ACCEPTED
- Decision: ACCEPTED
- Implementation: `323d53a1e80d9e20b7369648453419ba31f5df2a`
- Exporter Implementation Commit: `fd4a30e98ea1afa91fdd0d286d9407d40310d928`
- Integration Implementation SHA: `fd4a30e98ea1afa91fdd0d286d9407d40310d928`
- QA Task Commit: `773256025fe97e489a3dba88e37265b18de4f283`
- Audit Mirror: `ce712e5fae1988904ebd3cb64e460e717629f3bc`
- Tests: 169 / 169 PASS

## Exporter implementation

CX-018 adds a deterministic, fail-closed runtime exporter for accepted aligned PNG masters: fixed 128x128 RGBA resize, stable pivot, horizontal spritesheet packing, atlas metadata, runtime manifest, timing/hold-tick round-trip, pixel round-trip validation, package checksums, path containment, and staging preservation. The exporter does not extract video, curate frames, alter timing, or write to HuyenSu-TD.

## Input boundary

The Gate-17 branch contains the four source MP4s and sanitized accepted timing/VFX provenance, but no accepted aligned master PNG sequences. Because CX-018 explicitly forbids re-running extraction and forbids placeholders, no Trưng Trắc or Trưng Nhị runtime pack was fabricated. Calling the exporter without those masters fails closed with `RUNTIME_MASTER_MISSING`; no output directory was promoted.

### Known limitations

- Golden runtime packs remain pending delivery of the accepted aligned master PNG sequences from the Gate-17 production workspace.
- This repository is Python-only and has no `package.json`; `npm test` and `npm run build` cannot run here.

## Verification

- Python regression suite: 175 / 175 PASS.
- `git diff --check`: PASS.
- HuyenSu-TD: untouched.
- No source media or upstream production manifests were modified.

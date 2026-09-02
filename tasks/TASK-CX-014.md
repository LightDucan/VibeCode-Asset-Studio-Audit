# TASK-CX-014 — VFX Asset Library & Action Variant Binding

STATUS: READY_FOR_QA

Task: TASK-CX-014
Branch: `codex/task-cx-014-vfx-asset-library`
BASE: `d776e71f930cc9f174cb51fb9daf093a4d7ff46e`
Implementation Commit: `ef6b574dced8f4c194c36359630b5de47564240b`

## Scope

Implemented a reusable, filesystem-backed VFX asset library with immutable asset versions, deterministic content checksums, classification metadata, local-space definitions, defaults, and a sorted library index. Registration validates CX-013 curation and CX-012 alpha manifests without rewriting or copying source frames.

Implemented action variants that reference Base Motion and registered VFX assets, resolve binding/transform/timing/blend/layer overrides deterministically, and invoke the existing CX-012 compositor for derived composite output. Variant manifests retain asset and motion checksums, state, resolved values, and stale detection. Base Motion, curated VFX, and alpha PNGs remain shared and immutable.

Added lightweight VFX library and action-variant workspaces, exporter support for asset/index/variant evidence, and public fixtures containing two variants sharing one motion checksum while using distinct reusable VFX assets and composite checksums.

Milestone: BASIC MOTION + VFX + TIMING (project remains open; CX-015 is not started).

Tests: 133 passed, 0 failed.

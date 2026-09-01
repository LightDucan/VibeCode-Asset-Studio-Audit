# TASK-CX-006 — Frame Curation Assistant

STATUS: READY_FOR_QA
BASE: `e931553846e648a9c57e00dabb7bb0b35951c341`
Branch: `codex/task-cx-006-frame-curation`
Commit SHA: `79a98e7b5bbeab39f3d53534342d718c5c03ae8c`

Implemented Step 06 `frame_curation` as a deterministic, metadata-only assistant.
The service analyzes only Step-05 KEEP/KEY candidates, preserves immutable Step-04
and Step-05 manifests, computes exact/near/static/blur/suspicious suggestions,
supports protected KEY decisions, resolution undo/redo, similarity groups, timing-
safe previews, stale-source detection, persistence, and explicit advancement to
`background_removal`. A dependency-free browser workspace provides candidate
filmstrip, filters, progress, and group-compare metadata.

Tests: 84 tests passed, 0 failed.

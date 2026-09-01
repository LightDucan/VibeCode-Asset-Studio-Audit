# TASK-CX-005F — GitHub Privacy Architecture + Gate-05 Follow-up

STATUS: READY_FOR_QA

BASE (CX-005): `38f7bb490a725bf97736449d6bc2ad50e797b0ca`
AG-005: `5754110888ea91712281a0aac82de2b84304f85a`

The canonical repository remains the private production source. This task adds the missing Step-05 side-panel metadata and establishes a fail-closed, deterministic exporter for a separate public audit mirror. The exporter emits task/QA report text and JSON metadata only: commit SHAs, changed-file paths, diff statistics, test summaries, artifact hashes, and known limitations. It never exports source diffs, source files, binaries, media, credentials, or local absolute paths.

The public mirror is `LightDucan/VibeCode-Asset-Studio-Audit`. Its README documents that it is a metadata/reporting mirror and that the canonical repository is private. Publishing is performed with the authenticated GitHub CLI through `scripts/publish_audit_snapshot.py`; the publisher scans every output file and fails closed on binaries, secret-like values, absolute local paths, or source-directory payloads.

## Verification

Step-05 now renders the selected frame's PTS/timestamp and Step-04 source dimensions in the side panel. Values are read from the existing `frames.json` and are not duplicated or rewritten. Master frames, thumbnails, checksums, timestamps, and `frames.json` remain immutable.

The suite reports **73 tests passed, 0 failures** (the previous 72 remain green; one new metadata regression test was added). Exporter tests cover deterministic output, task identity, SHA/path/stat metadata, artifact hashes, source-content exclusion, unsafe binary/secret/absolute-path rejection, and repeated export stability.

AG-004 remains explicitly `REPORT_RECOVERY_REQUIRED`; no historical report is fabricated. The evidence gap is carried into the audit snapshot as a known limitation.

## Known limitations

- Historical AG-004 report recovery remains an evidence gap; this task does not replace it with a fabricated report.

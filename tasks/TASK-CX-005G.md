# TASK-CX-005G — Audit Snapshot Parser Fix

STATUS: READY_FOR_AUDIT
BASE: `e2c5c552c72f0e833290c26e56a2590e2f502795`
Branch: `codex/task-cx-005g-audit-parser-fix`
Commit SHA: `e931553846e648a9c57e00dabb7bb0b35951c341`

Corrected the metadata-only audit exporter so explicit P0–P3 severity counters are parsed as `issue_severity_summary`, while only actual entries in a Known Limitations section populate `known_limitations`. Added regression coverage for zero and non-zero counters, section isolation, and independent QA/CX provenance. No production pipeline or Frame Review code was modified.

Tests: 79 tests passed, 0 failed. The corrected AG-005R snapshot retains its own QA branch and commit identity; CX-005G is published separately.

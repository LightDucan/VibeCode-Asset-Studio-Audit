# TASK-CX-011 — PNG Sequence Export

STATUS: READY_FOR_QA
BASE: `32a32b899454de4f6211f8c3407ea4c9d2baef1d`
Branch: `codex/task-cx-011-png-sequence-export`
Implementation Commit: `c1ef6e8f72bf774917d8222129e0ab8bab2373c2`

Implemented the final original 11-step MVP stage `png_sequence_export`.
The exporter consumes only the accepted Step-10 preview contract, copies each
aligned RGBA PNG byte-for-byte exactly once, preserves sequence/source frame
identity and timing metadata, validates hashes/dimensions/alpha, supports
FAIL_SAFE, REPLACE_EXPORT and NEW_VERSION destinations, and uses staging with
atomic promotion. `verify_export` supports portable moved packages. A compact
export workspace exposes destination, format, canvas, pivot, timing, size and
verification status. No source asset, timing value, alignment, alpha or pivot
is modified; no VFX work is included.

MOTION PIPELINE MVP COMPLETE (Steps 01–11).

Tests: 114 tests passed, 0 failed.

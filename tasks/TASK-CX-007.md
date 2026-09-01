# TASK-CX-007 — Background Removal

STATUS: READY_FOR_QA
BASE: `2f9b46edec60aba46c6e2678927e44bd5d724a73`
Branch: `codex/task-cx-007-background-removal`
Implementation Commit: `287d5ec8f0c1024cb0c25707593347c81c9ed1a1`

Implemented Pipeline Step 07 `background_removal` with a formal provider
contract and deterministic `BorderConnectedBackgroundRemovalProvider`. The
stage consumes only Step-06 retained frames, preserves source identity/timing,
keeps meaningful source alpha, removes only border-connected near-background
regions, emits same-size RGBA PNGs, records per-frame alpha metrics and
sequence warnings, detects stale inputs/profiles, and atomically promotes a
fully verified run. A lightweight inspection workspace supports source/result,
alpha and contrasting-background views. Step 08 receives ordered references;
no alignment logic is performed here.

Tests: 92 tests passed, 0 failed.

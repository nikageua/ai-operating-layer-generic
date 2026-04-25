# Core Migrations

Use this file to track breaking changes in AIL core structure and contracts.

## v1 → v2

### Structural changes
- replaced many v1 folders with `core/`, `project/`, and `runtime/`
- removed `brain/` current-truth files as central coordination mechanism
- removed mandatory `epics/` flow as a default operating requirement
- removed metaharness-heavy workflow from the core path

### Behavioral changes
- introduced Tiny / Standard / Architectural lanes
- replaced status-heavy memory with attempt-memory + promoted learnings
- replaced tracked local paths with logical repo and env IDs
- replaced copying the whole AIL per story with story folders inside one shared AIL structure

### Migration guidance
- move stable, reusable doctrine into `core/`
- move repo-specific conventions, patterns, and constraints into `project/`
- keep local path/env resolution in `runtime/local-map.yaml`
- archive or discard old `brain/` state instead of trying to preserve it as live truth
- keep only the v1 artifacts that still provide real decision support

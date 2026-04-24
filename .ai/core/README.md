# AIL Core

This directory contains the updateable, generic operating model of AIL v2.

## What belongs in `core/`

Use `core/` for reusable operating doctrine:
- lane selection rules
- architecture sanity checks
- failure handling rules
- task, spec, and spike templates
- profile schema
- migration notes
- examples that teach the operating model itself

## What does not belong in `core/`

Do not put these here:
- project-specific commands
- local machine paths
- localhost URLs
- repo-specific quirks
- one-off historical notes

Those belong in either `project/` or `runtime/`.

## Boundary model

- `core/` is upstream and replaceable
- `project/` is project-specific and shareable
- `runtime/` is local, volatile, and machine-specific

If a file changes mainly because one repo or one workstation is different, it does not belong in `core/`.

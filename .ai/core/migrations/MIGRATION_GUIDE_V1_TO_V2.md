# Migration Guide: v1 to v2

## Intent
This migration is not just a folder rename. It is a shift from governance-heavy coordination to execution-first structure with focused learning.

## What to stop carrying forward blindly
- current-truth brain files
- heavyweight status flows for every task
- machine-specific details in tracked docs
- per-story copies of the whole AIL

## What to preserve
- useful templates
- real architecture constraints
- proven patterns
- repeated pitfalls
- stable project context

## Practical migration steps
1. Create `core/`, `project/`, and `runtime/`.
2. Move reusable project knowledge into `project/`.
3. Archive old `brain/` state instead of preserving it as live truth.
4. Convert cross-repo initiatives into story folders.
5. Replace local paths in tracked docs with logical repo IDs.
6. Keep runtime mapping local.

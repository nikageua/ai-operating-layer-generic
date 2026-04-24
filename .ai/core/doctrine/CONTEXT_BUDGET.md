# Context Budget

AIL doctrine should be loaded selectively.

## Rules
- bootstrap with Tier 0 only
- load project files only when a triggering signal exists
- stop loading once the current decision is clear
- prefer narrow reads over loading large files wholesale
- do not keep reading because a file exists

## Practical test
If a file will not change the next decision, do not load it.

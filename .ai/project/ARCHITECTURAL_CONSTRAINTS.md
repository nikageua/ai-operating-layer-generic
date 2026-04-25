# Architectural Constraints

Capture hard boundaries, forbidden shortcuts, and migration-sensitive areas.

Good entries:
- ownership boundaries between repos
- layering rules that must not be broken
- legacy modules requiring special migration handling
- security-sensitive flows that must stay centralized


## Placement rule

Use this file for small, stable architectural rules that should be loaded early.

Use `project/decisions/` for richer architectural decisions with context and trade-offs.
Use story files for architecture notes specific to one story.
Do not create free-floating top-level architecture docs unless there is a very strong reason.

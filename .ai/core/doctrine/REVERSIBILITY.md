# Reversibility

Not all small changes are equally safe.
AIL should consider not only size and complexity, but also how reversible a change is.

## Two-way door
Easy to undo.
Examples:
- text change
- local UI tweak
- private refactor with low blast radius

## One-way door
Expensive or risky to undo.
Examples:
- published API contract change
- event schema change
- database migration
- permission model change
- external dependency introduction

## Rule
If a change is effectively one-way, treat it more cautiously than its raw size suggests.
A seemingly small but irreversible change may deserve a higher lane or a stop-and-ask moment.

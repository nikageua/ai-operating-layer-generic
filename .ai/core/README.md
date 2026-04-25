# AIL Core

This directory contains the updateable, generic operating model of AIL v2.

## Structure
- `doctrine/` — behavioral rules and operating doctrine
- `templates/` — reusable artifact templates
- `references/` — supporting contracts and reference docs
- `migrations/` — migration notes and transition guidance
- `examples/` — compact examples showing the operating model in practice

## How to use core efficiently
Do not read all of `core/` by default.
Start with:
- `DOCTRINE_NAVIGATION.md`
- `doctrine/LANES.md`
- `doctrine/FAILURE_PROTOCOL.md`
- `doctrine/UPDATE_GOVERNANCE.md`

Then pull in only the doctrine that changes the current decision.

## Boundary rule
If a file changes mainly because one repo, one developer, or one workstation is different, it does not belong in `core/`.

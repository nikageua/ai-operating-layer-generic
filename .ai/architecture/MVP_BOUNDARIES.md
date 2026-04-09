# MVP Boundaries

> **Deprecated.** MVP scope is now declared inside each epic.
>
> See `.ai/epics/` — each epic has a `## MVP Scope` field that declares
> whether it is `MVP`, `Post-MVP`, or `Nice-to-have`, along with the minimum
> delivery bar for that slice.
>
> This file is retained for reference only. Do not add new content here.

## Why This Changed

Previously, MVP scope was defined once globally here.
This did not scale across multiple features, specs, and repositories.

MVP is now a property of each epic, defined when the epic is created from an
approved spec. This lets different features have different MVP bars, and lets
the orchestrator agent reason about which epics to prioritize.

## Anti-Scope-Creep Rule (still applies)

Even with per-epic MVP scope, the rule holds:
if a task does not directly advance the active epic's stated goal, it must not be included.

Scope creep at the task level is caught by the sub-agent profile's `## Constraints` section
and enforced by the one-active-task rule in `AGENTS.md`.

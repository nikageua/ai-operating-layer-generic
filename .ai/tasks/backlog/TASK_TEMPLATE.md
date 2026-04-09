# TASK_ID — Task Title

## Epic
[EPIC_ID or `standalone`]

## Agent Profile
[profile-id from `.ai/agents/profiles/`]
If the profile does not exist, run the harness bootstrap protocol first.

## Goal
[Exact, specific goal — what does done look like?]

## Why
[Why this task matters within the active epic]

## Scope

### In Scope
- [specific file, component, or behavior to change]
- [specific file, component, or behavior to change]

### Out of Scope
- [anything the sub-agent must NOT touch]
- [anything deferred to a later task]

## Acceptance Criteria
All criteria must be verifiable by the sub-agent before marking done.

1. [criterion — specific and testable]
2. [criterion]
3. [criterion]

## Files Likely Affected
- [file or area — helps sub-agent scope its search]
- [file or area]

## Constraints For Sub-Agent
- Keep scope small. Do not refactor beyond the stated goal.
- Do not modify files outside the In Scope list without approval.
- Confirm the harness (bootstrap + validate + test) still passes after changes.
- If the active profile fails, trigger Tier 1 metaharness optimization before retrying.

## Deliverable
[What artifact, behavior, or state change constitutes completion]

## Tags
`[spike]` | `[harness]` | `[frontend]` | `[backend]` | `[infra]` | `[docs]`
(remove tags that don't apply)

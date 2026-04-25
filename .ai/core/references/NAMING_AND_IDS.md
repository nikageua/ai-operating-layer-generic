# Naming and IDs

AIL v2 must support concurrent work by multiple developers and agents.
Sequential filenames like `TASK-001.md` are not safe in distributed creation flows.

## Rule
Use collision-resistant filenames and separate them from the human-readable title.

### Recommended filename shape

```text
<type>-<utc-timestamp>-<short-slug>-<shortid>.md
```

Examples:
- `task-20260421-160812-resend-confirmation-email-a7k3.md`
- `story-20260421-161025-user-invite-flow-j9d2.md`
- `spec-20260421-161144-auth-refresh-contract-p4lm.md`
- `spike-20260421-161302-token-ownership-r8q1.md`

## Required parts

- **type**: `task`, `story`, `spec`, `spike`, `proposal`
- **utc-timestamp**: creation time in UTC, enough precision to reduce collisions
- **short-slug**: short human-readable intent
- **shortid**: 4-8 characters of randomness or actor-safe uniqueness

## File vs title

- filename: machine-safe and collision-resistant
- title inside file: human-readable

Example:

```md
# TASK: Resend confirmation email
ID: task-20260421-160812-resend-confirmation-email-a7k3
```

## Anti-patterns

Do not use:
- `TASK-001.md`
- `STORY-004.md`
- counters that require global coordination
- filenames that rely only on a title slug

## Why this matters

With multiple developers or agents creating artifacts in parallel, low-entropy naming guarantees merge conflicts.
Collision-resistant IDs let tracked docs be created independently.

# AI Operating Layer Generic

A portable execution and learning layer for AI-assisted software delivery.

## What this is

AIL v2 is a lightweight but opinionated coordination layer for AI-assisted software work across one or more repositories.

It is designed to:
- preserve structure where it matters,
- stay lightweight where it does not,
- learn from failed attempts,
- work across multiple repositories using logical IDs,
- evolve centrally without constantly breaking local project overlays,
- and change durable truth through a semi-automatic governance model.

## Why this exists

AI is strong at local implementation but weak at preserving system intent over time.
Without operating structure, teams get speed at the cost of drift, repetition, boundary mistakes, and fragile delivery.

AIL v2 is designed to solve that without falling into governance-heavy ceremony.

## The operating model

```text
Change request
  ↓
Lane selection (Tiny / Standard / Architectural)
  ↓
Architecture sanity check (for non-trivial work)
  ↓
Story/task execution using logical repo IDs
  ↓
Failure-aware learning loop when blocked
  ↓
Candidate proposal capture in runtime
  ↓
Main-agent curation
  ↓
Human approval for durable changes
  ↓
Promotion into project/core truth
```

## Semi-automatic evolution

AIL v2 does not rely on silent self-mutation.
It evolves through a semi-automatic model:

- runtime learning is fast,
- sub-agents can capture candidate updates,
- main agent curates what is worth promotion,
- human approval gates durable truth.

This keeps learning alive without allowing uncontrolled drift.


See also: `.ai/core/references/NAMING_AND_IDS.md` for collision-resistant artifact naming.

## Shared team operation

For real parallel team usage, AIL v2 also defines doctrine for:
- parallel work model
- knowledge scopes
- runtime lifecycle
- conflict resolution
- ownership
- cross-repo impact discovery
- operating-layer health
- anti-bloat
- gradual adoption

## Token efficiency

AIL v2 is designed to be read selectively. The full doctrine is not the default context for every session. Use the navigation and read-tier rules to keep context small.

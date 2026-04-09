# Harness Update Protocol

Harness files can be updated at three levels of autonomy.
The level depends on what is being changed and how risky it is.

---

## Tier 1 — Automatic (no approval needed)

The metaharness optimization loop runs automatically within a task session.
The agent may:

- run `metaharness run` against the current profile
- evaluate candidates using `tasks.json`
- select the best candidate within the run

These are in-memory / run-scoped operations. Nothing is written back to `.ai/` yet.

**When this happens:**
- after every sub-agent task completes on a `draft` or `validated` profile
- when a sub-agent task fails and the failure looks harness-related (exit code from
  bootstrap, validate, or test scripts — not from the task implementation itself)

---

## Tier 2 — Proposal Required (human approves)

The agent must propose and wait for approval before:

- promoting a metaharness run candidate back into `.ai/agents/profiles/[id].md`
- changing the profile `Status` field (e.g. `draft → validated`)
- adding or removing entries in the profile's `## Key Instructions` section
- updating `## Known Pitfalls` based on new failures observed

Proposal format:

```
Proposed harness update:

Profile: [profile-id]
Change: [what is changing and why]
Evidence: [which metaharness run or task failure triggered this]
Diff:
  - old: [old content]
  + new: [new content]

Approve harness update? (Yes / No)
```

Only after `Yes` may the agent write to the profile file.

---

## Tier 3 — Always Manual

The following must never be modified by the agent without explicit human instruction:

- `tasks.json` acceptance criteria (adding, removing, or reweighting checks)
- profile `Status` set to `stable` or `deprecated`
- `HARNESS_BOOTSTRAP.md` — the bootstrap protocol itself
- `HARNESS_UPDATE_PROTOCOL.md` — this file

These define the rules of the system. Changing them requires deliberate human intent,
not an automated optimization pass.

---

## How Harness Rules Evolve From Nothing

At project start, profiles do not exist. Here is how they emerge:

```
1. Spec is approved → epics identified → first task needs a profile
2. Harness bootstrap protocol runs (see HARNESS_BOOTSTRAP.md)
   → agent inspects target repo → generates draft profile
3. A harness validation task runs the initial baseline
   → confirms bootstrap/validate/test scripts work
   → profile moves from bootstrap → draft
4. Sub-agents execute real tasks against the draft profile
   → metaharness runs Tier 1 optimization after each task
   → when score improves, agent proposes Tier 2 update to profile
5. After N successful tasks, profile is proposed for stable via Tier 2
6. Human approves → profile is stable
```

This means harness rules are **discovered empirically**, not defined upfront.
The system starts with a thin bootstrap and gets smarter with every task run.

---

## Harness Score

Each metaharness run produces a score from `tasks.json` (sum of weights of passing checks).
Track the score in the profile's `## Metaharness Optimization History` section.

Target thresholds:
- `draft → validated`: score ≥ 70% of max possible score
- `validated → stable`: score = 100% on at least 3 consecutive runs

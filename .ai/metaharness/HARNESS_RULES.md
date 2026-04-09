# Harness Rules

These rules govern how agents read, maintain, and improve the harness files in this repository.

---

## What Is The Harness

The harness is the set of files that instruct and support the coding agent's workflow.
It includes:

- `AGENTS.md` — primary instruction file for coding agents
- `GEMINI.md` (if present) — instruction file for Gemini CLI
- `scripts/bootstrap.sh` — environment setup
- `scripts/validate.sh` — static/structural validation
- `scripts/test.sh` — functional test runner

---

## Rule 1: Never Break The Harness

Any task that touches harness files must leave the harness in a passing state.

Before completing a task that modifies harness files, verify:
1. `scripts/bootstrap.sh` exits 0
2. `scripts/validate.sh` exits 0
3. `scripts/test.sh` exits 0

If verification tools are not available in the current environment, note this explicitly
and flag it as a required follow-up before the task moves to `review`.

---

## Rule 2: Harness Changes Require Explicit Scope

Harness files may only be modified if the active task's scope explicitly includes them.

If a harness file needs updating but the current task does not cover it:
- do not modify the file silently
- propose a new `[harness]` task for the change and wait for approval

---

## Rule 3: tasks.json Is The Source Of Truth For Acceptance

`tasks.json` defines the measurable acceptance criteria for the harness.
When proposing changes to harness files, verify that all items in `tasks.json` still pass.

When a harness improvement introduces new acceptance requirements:
- propose an update to `tasks.json` as part of the AI layer update proposal
- do not modify `tasks.json` without human approval

Full schema, ownership rules, scoring thresholds, and when to add/remove checks:
see `.ai/metaharness/TASKS_JSON_SPEC.md`.

---

## Rule 4: Metaharness Loop Before Major Harness Refactors

For large harness changes (restructuring `AGENTS.md`, rewriting scripts),
prefer running the metaharness optimization loop over manual editing:

```
metaharness run . --backend <backend> --budget <n> --run-name <name>
```

Review the run artifacts under `runs/` and promote the best candidate.
Do not apply metaharness-generated changes directly without reviewing the diff.

---

## Rule 5: Harness Snapshot On Milestone Completion

When an epic is moved to `done`, record a snapshot of the current harness state
in `.ai/metaharness/snapshots/` using the format:

```
EPIC_ID_harness_snapshot.md
```

This preserves a baseline for future optimization runs.

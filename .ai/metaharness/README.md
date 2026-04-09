# Metaharness

This layer integrates the `metaharness` optimization framework into the AI operating layer.

## What Is Metaharness

Metaharness runs an outer optimization loop around the *harness* — the files that wrap and
instruct an AI coding agent. This includes instruction files, setup scripts, validation
scripts, and test scripts.

The loop works like this:

1. Start from a baseline harness (e.g. current `AGENTS.md`, `scripts/`)
2. Ask a coding agent to propose improvements to the harness files
3. Validate and evaluate the result against `tasks.json` acceptance criteria
4. Keep the best candidate
5. Store all artifacts on disk for review

## Why It Belongs Here

Many agent failures come from the harness, not the model:

- weak or missing instructions in `AGENTS.md`
- broken bootstrap or validation scripts
- acceptance checks that do not reflect the actual task
- missing environment setup steps

Metaharness turns these artifacts into a measurable, repeatable optimization target.

## Files In This Layer

| File | Purpose |
|------|---------|
| `HARNESS_RULES.md` | Agent rules for maintaining and improving harness files |
| `metaharness.template.json` | Template for a project's `metaharness.json` config |
| `tasks.template.json` | Template for a project's `tasks.json` evaluation criteria |

## How To Use

1. Copy `metaharness.template.json` to your project root as `metaharness.json` and fill in the fields.
2. Copy `tasks.template.json` to your project root as `tasks.json` and define your acceptance checks.
3. Run `metaharness run . --backend <backend> --budget <n>` to start an optimization loop.
4. Review the run artifacts under `runs/` and promote the best candidate manually.

## Relationship To Tasks And Epics

Harness improvements are tracked as regular tasks in `.ai/tasks/`.
Tag harness-related tasks with the label `[harness]` in their title so they are easy to filter.

When a harness improvement task is completed:
- update `tasks.json` to reflect any new acceptance criteria
- verify the harness still passes `metaharness run` with the fake backend before committing

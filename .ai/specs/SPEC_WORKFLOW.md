# Spec Workflow

This document defines how a feature moves from raw description to implemented code.

---

## Stage 0: Feature Seed

The human provides a short feature description — even a single sentence is enough.
The AI agent's job at this stage is NOT to start building, but to ask clarifying questions
and co-author the spec.

Trigger phrase: "I want to build [feature description]"

The agent must:
1. Create a new spec file from `SPEC_TEMPLATE.md` in `.ai/specs/draft/`
2. Fill in the Feature Description from the human's input
3. Identify gaps and ask targeted questions (one round at a time)
4. NOT create epics, tasks, or architecture decisions yet

---

## Stage 1: Spec Drafting (draft → review)

The agent works with the human to fill out the spec template iteratively.

Required sections before moving to `review`:
- Problem Statement
- Goals (at least 2)
- Non-Goals (at least 1)
- User Stories (at least 2)
- Acceptance Criteria (at least 3, in Given/When/Then format)
- Affected Repositories / Frameworks (all repos identified)
- Open Questions resolved or explicitly deferred

When complete, the agent proposes:

```
Proposed AI layer update:

Specs
- move SPEC_xxx from draft → review

Approve? (Yes / No)
```

---

## Stage 2: Architecture Review (review → approved)

Once the spec is in review, the agent:

1. Reads `.ai/architecture/ARCHITECTURE_DECISIONS.md`
2. Identifies if any open architectural questions exist
3. If yes → proposes spike tasks in `.ai/tasks/backlog/` tagged `[spike]`
4. If no → proposes moving spec to `approved` and spawning epics

Spike tasks are executed like normal tasks. When all spikes are done, architecture
notes are added to the spec and it moves to `approved`.

---

## Stage 3: Epic Breakdown (approved)

When a spec is approved, the agent breaks it into epics.

Rules for epic breakdown:
- Each epic must deliver a meaningful, independently testable slice of the feature
- Epics must respect repository boundaries — one epic should not span too many repos
- Each epic gets an entry in `.ai/epics/EPIC_INDEX.md` and a file in `.ai/epics/backlog/`
- The spec file is updated with the `## Epics Spawned` table

MVP scope is declared inside each epic (see EPIC_TEMPLATE.md).

---

## Stage 4: Task Breakdown (per epic)

When an epic is activated (moved to `in-progress`), the agent breaks it into SMART tasks.

SMART task rules:
- **Specific** — describes exactly one code change or deliverable
- **Measurable** — has clear acceptance criteria
- **Achievable** — completable in one sub-agent session
- **Relevant** — directly advances the active epic
- **Time-bounded** — scoped small enough to complete without branching

Each task declares:
- its parent epic
- the sub-agent profile it requires (see `.ai/agents/profiles/`)

---

## Stage 5: Sub-Agent Execution

Sub-agents pick up tasks from `.ai/tasks/in-progress/`.
Each sub-agent reads its assigned profile from `.ai/agents/profiles/` before acting.
The harness for each sub-agent is maintained by the metaharness layer.

---

## Stage 6: Spec Completion (implemented)

When all epics spawned from a spec are `done`, the spec moves to `implemented`.
The agent proposes this transition as part of the final epic's AI layer update.

# AI Agent Operating Rules

This document defines how AI agents must operate inside this repository.

The goal is to ensure stable incremental development and prevent uncontrolled scope expansion.

---

# 1. Core Principles

## Build the smallest working slice
Prefer:
small working systems
over
large incomplete systems.

## Respect task boundaries
Agents must only implement the current active task.

The active task is defined in:
`.ai/brain/CURRENT_FOCUS.md`

Agents must not implement future systems unless explicitly instructed.

## Avoid premature complexity
Do not introduce:
- large frameworks
- speculative architecture
- future systems
- unnecessary abstractions

## Prefer clarity over cleverness
Code should prioritize:
- readability
- maintainability
- small changes
- clear intent

## Preserve extensibility
Avoid tightly coupling low-level systems.
Keep responsibilities separate where practical.

---

# 2. Read Before Acting

Before implementing any change, the agent must read:

- `.ai/project/PROJECT_CONTEXT.md`
- `.ai/project/CURRENT_STATUS.md`
- `.ai/architecture/MVP_BOUNDARIES.md`
- `.ai/architecture/ENGINE_DECISIONS.md`
- `.ai/agent/AGENTS.md`
- `.ai/brain/CURRENT_FOCUS.md`
- `.ai/brain/PROJECT_STATE.md`
- `.ai/brain/DECISIONS_LOG.md`
- `.ai/brain/NEXT_STEPS.md`
- `.ai/brain/OPEN_QUESTIONS.md`
- `.ai/tasks/TASK_INDEX.md`
- `.ai/tasks/TASK_SELECTION_RULES.md`
- `.ai/tasks/in-progress/*`
- `.ai/memory/*`

If the AI layer appears out of sync with the repository, the agent must pause implementation and propose synchronization first.

---

# 3. One Active Task Rule

Only one task may exist in:
`.ai/tasks/in-progress/`

Agents must not combine multiple roadmap items into one implementation.

---

# 4. AI Operating Layer Update Protocol

The `.ai/` directory acts as the AI operating system of the repository.

It must never be modified silently.

All updates require explicit human approval.

This applies to:
- `.ai/brain/`
- `.ai/tasks/`
- `.ai/memory/`

## Update Workflow

When repository state changes after a task, the agent must:
1. detect which `.ai` files require updates
2. generate a concise proposal
3. request approval

Preferred proposal format:

Proposed AI layer update:

Tasks
- ...

Brain
- ...

Memory
- ...

Approve AI layer update? (Yes / No)

Only after explicit `Yes` may the agent apply changes.

## Update batching
All `.ai` updates must be grouped into one approval request.

## Commit Rules
If approved, the agent may:
- modify `.ai` files
- move task files
- create a single commit

Commit message format:
`AI: sync AI operating layer after TASK_xxx`

---

# 5. Task Autopilot Protocol

After a task is completed and accepted, the agent may propose the next task from:
`.ai/tasks/ready/`

The agent must not automatically start the next task.

Instead, it must:
1. inspect current project state
2. inspect `.ai/brain/NEXT_STEPS.md`
3. inspect `.ai/tasks/ready/`
4. identify the best next task candidate
5. propose a task transition for approval

Proposal format:

Proposed next task:

- current task completed: TASK_xxx
- recommended next task: TASK_yyy
- reason:
  - ...
  - ...

Proposed AI layer update:

Tasks
- move TASK_xxx from review → done
- move TASK_yyy from ready → in-progress

Brain
- CURRENT_FOCUS.md → set active task to TASK_yyy
- NEXT_STEPS.md → reorder priorities if needed

Approve task transition? (Yes / No)

Only after `Yes` may the agent move a task from `ready/` to `in-progress/`.

---

# 6. Project-Specific Scope Reminder

This section should be customized per repository.

Add:
- what systems are in scope
- what systems are explicitly out of scope
- what current milestone matters most

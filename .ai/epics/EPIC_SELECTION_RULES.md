# Epic Selection Rules

Epics sit above tasks in the work hierarchy.
A task must always belong to an epic (or be explicitly marked as standalone).

## When selecting the next epic, prefer:

1. the epic most aligned with the current project milestone
2. the epic with the highest ratio of ready tasks to blocked tasks
3. epics that unblock other epics downstream
4. smaller, more focused epics over large multi-month initiatives

## Avoid activating an epic if:

- its tasks are not yet defined or broken down
- it conflicts with the scope of an already active epic
- it depends on unresolved architecture decisions in `.ai/architecture/`

## Epic lifecycle:

1. Epics start in `backlog/`
2. When tasks are defined and scope is clear, move to `ready/`
3. When the first task of an epic is activated, move the epic to `in-progress/`
4. When all tasks are done and output is reviewed, move to `review/`
5. After human approval, move to `done/`

## One active epic rule:

Only one epic should be `in-progress/` at a time unless explicitly approved otherwise.

## Relationship to tasks:

- Every task file should declare its parent epic via the `Epic` field in its header.
- If no epic applies, the task must be marked `epic: standalone`.
- Agents must not work on tasks belonging to a `backlog` epic.

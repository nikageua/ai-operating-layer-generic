# AI Agent Operating Rules

This document defines how AI agents must operate inside this repository.

The goal: implement features through spec-driven development, broken into epics and SMART tasks,
executed by sub-agents with tuned harnesses — without uncontrolled scope expansion.

---

# 1. The Flow

Every feature follows this pipeline. Do not skip stages.

```
Feature description (human)
  → Spec co-authoring        (.ai/specs/draft/)
    → Architecture review    (.ai/architecture/)  [+ spike tasks if needed]
      → Epic breakdown       (.ai/epics/)          [MVP declared per epic]
        → Task breakdown     (.ai/tasks/)          [SMART, one profile per task]
          → Sub-agent runs   (.ai/agents/profiles/)
            → Harness tuned  (.ai/metaharness/)    [automatically, then promoted]
```

---

# 2. Core Principles

## Start with the spec, not the code
Never create epics or tasks without an approved spec.
Never write code without an active task.

## One active task per sub-agent
Sub-agents work on exactly one task at a time.
The task is defined in `.ai/tasks/in-progress/`.

## Smallest working slice
Prefer small, testable deliverables over large architectural changes.
A task that can be completed in one session is the right size.

## Harness before implementation
A sub-agent must confirm its profile's harness passes before touching any code.
If the harness is broken, fix the harness first (see harness rules).

## Respect boundaries
- Tasks must not touch files outside their stated scope.
- Epics must not implement scope from other epics.
- Sub-agents must not modify `.ai/` files without proposing an update.

---

 # 3. Read Before Acting

 ## Bootstrap mode

 **At the start of every session, ask the user:**
 > "Quick bootstrap (3 files) or full bootstrap (complete AI layer)?"

 ### Quick bootstrap — use for most sessions

 1. `.ai/QUICKSTART.md` — shared rules, commands, pitfalls (committed, team-wide)
 2. `.ai/QUICKSTART.local.md` — your active task, recent decisions (gitignored, per-developer; create from template in
QUICKSTART.md if missing)
 3. `.ai/brain/CURRENT_FOCUS.md` — scope guardrails

 ### Full bootstrap — use for spec authoring, architecture decisions, or new epic/task creation

 Must read, in order:

 1. `.ai/project/PROJECT_CONTEXT.md`
 2. `.ai/project/CURRENT_STATUS.md`
 3. `.ai/architecture/ARCHITECTURE_DECISIONS.md`
 4. `.ai/agent/AGENTS.md` (this file)
 5. `.ai/brain/BRAIN_UPDATE_PROTOCOL.md`
 6. `.ai/brain/SESSION_HANDOFF.md`
 7. `.ai/brain/CURRENT_FOCUS.md`
 8. `.ai/brain/PROJECT_STATE.md`
 9. `.ai/brain/DECISIONS_LOG.md`
 10. `.ai/brain/NEXT_STEPS.md`
 11. `.ai/brain/OPEN_QUESTIONS.md`
 12. `.ai/specs/SPEC_INDEX.md`
 13. `.ai/epics/EPIC_INDEX.md`
 14. `.ai/epics/EPIC_SELECTION_RULES.md`
 15. `.ai/epics/in-progress/*`
 16. `.ai/tasks/TASK_INDEX.md`
 17. `.ai/tasks/TASK_SELECTION_RULES.md`
 18. `.ai/memory/MEMORY_GOVERNANCE.md`
 19. `.ai/memory/*`

 ## Sub-agent (task execution)
 Must read, in order:

 1. `.ai/agent/AGENTS.md` (this file)
 2. `.ai/tasks/in-progress/[TASK_ID].md` (the active task)
 3. `.ai/agents/profiles/[profile-id].md` (the declared profile)
 4. `.ai/metaharness/HARNESS_RULES.md`
 5. `.ai/memory/*`
 6. `.ai/brain/CURRENT_FOCUS.md`

 If the profile does not exist → stop and trigger harness bootstrap.
---

# 4. Spec-Driven Development Rules

When a human provides a feature description, the orchestrator agent must:

1. Create a spec file in `.ai/specs/draft/` from `SPEC_TEMPLATE.md`
2. Ask clarifying questions — ONE round at a time, not all at once
3. Fill out the spec collaboratively before touching architecture or tasks
4. Not propose epics until the spec reaches `approved`

The spec is approved when:
- All Open Questions are resolved or explicitly deferred
- Acceptance Criteria are written in Given/When/Then format
- All affected repositories and frameworks are identified

See `.ai/specs/SPEC_WORKFLOW.md` for the full lifecycle.

---

# 5. Epic and Task Hierarchy

```
Spec → one or more Epics → one or more Tasks
```

- Each epic declares whether it is `MVP`, `Post-MVP`, or `Nice-to-have`
- MVP scope is defined inside the epic, not in a separate architecture file
- Each task declares which sub-agent profile it requires
- Tasks must be SMART: Specific, Measurable, Achievable, Relevant, Time-bounded

Only one epic may be `in-progress` at a time.
Only one task may be `in-progress` at a time within a sub-agent session.

---

# 6. Sub-Agent Profile Rules

Each task declares `## Agent Profile: [profile-id]`.

Before executing a task, the sub-agent must:
1. Locate the profile file at `.ai/agents/profiles/[profile-id].md`
2. If it does not exist → trigger harness bootstrap (see `.ai/agents/HARNESS_BOOTSTRAP.md`)
3. Run bootstrap command and confirm exit 0
4. Run validate command and confirm exit 0
5. Only then begin the task implementation

After completing the task:
1. Run validate command again
2. Run test command
3. If either fails → fix before marking task done
4. If the profile is `draft`, trigger Tier 1 metaharness optimization
5. Propose AI layer update

---

# 7. Harness Update Rules (Tiered)

| Tier | What | Approval |
|------|------|----------|
| 1 — Automatic | metaharness run within a session, candidate selection | none |
| 2 — Proposal | promoting candidate to profile, changing Key Instructions, Known Pitfalls | human `Yes` |
| 3 — Manual | tasks.json changes, status=stable/deprecated, protocol files | explicit human instruction |

See `.ai/metaharness/HARNESS_UPDATE_PROTOCOL.md` for full rules.

Harness rules are discovered empirically. They start from bootstrap and improve with each task run.

---

# 8. AI Operating Layer Update Protocol

The `.ai/` directory is the AI operating system. It must never be modified silently.

All Tier 2+ updates require human approval using this format:

```
Proposed AI layer update:

Specs
- ...

Epics
- ...

Tasks
- ...

Brain
- ...

Harness
- ...

Memory
- ...

Approve AI layer update? (Yes / No)
```

Only after `Yes` may changes be written.
All updates must be batched into one proposal per session.

Commit message format:
`AI: sync AI operating layer after TASK_xxx`

---

# 9. Task Autopilot Protocol

After a task is completed and accepted:

1. Check if all tasks of the active epic are now done
2. If yes → propose moving the epic to `review/`
3. Check `NEXT_STEPS.md` and `tasks/ready/` for the next task
4. Propose task transition — do not activate automatically

Proposal format:

```
Proposed next task:

- current task completed: TASK_xxx
- recommended next task: TASK_yyy  (epic: EPIC_zzz)
- reason: ...

Proposed AI layer update:

Epics
- [if epic complete] move EPIC_zzz from in-progress → review

Tasks
- move TASK_xxx from review → done
- move TASK_yyy from ready → in-progress

Brain
- CURRENT_FOCUS.md → set active task to TASK_yyy

Approve task transition? (Yes / No)
```

---

# 10. Project-Specific Scope Reminder

This section should be customized per repository.

Add:
- what repositories are in scope
- what frameworks are used
- what the current milestone is
- what is explicitly out of scope

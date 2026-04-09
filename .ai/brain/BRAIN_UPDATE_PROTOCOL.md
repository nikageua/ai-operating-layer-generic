# Brain Update Protocol

This document defines exactly when each brain file is updated, who updates it, and what format to use.

Brain files represent the **current working state** of the project.
They are living documents — stale brain files are worse than no brain files.

---

## Who Can Update Brain Files

| Role | May propose updates | May apply updates |
|------|---------------------|-------------------|
| Orchestrator agent | Yes | Only after human `Yes` |
| Sub-agent | Yes (for files in its scope) | Only after human `Yes` |
| Human | Yes | Directly, at any time |

All agent-initiated brain updates must be batched into the standard AI layer update proposal
(see `AGENTS.md` Section 8). Brain updates are never applied silently.

---

## File-by-File Rules

---

### SESSION_HANDOFF.md

**Purpose:** Lets a new agent session pick up exactly where the last one left off.

**When to update:**
- **End of every session** — before the conversation closes, the orchestrator must update this file.
- **Start of a new session** — the agent reads this file first, then verifies it is still accurate.

**What triggers an update:**
- Any change to the active task
- Any change to the active epic
- Any unresolved issue or blocker discovered during the session
- Any file that must not be touched (added to do-not-touch list)

**Who updates it:** Orchestrator agent, proposed at session end. Human may edit directly.

**Minimum required fields after each session:**
```
- Current active task (TASK_ID or "none")
- Current active epic (EPIC_ID or "none")
- Last action taken
- What was left incomplete and why
- Do-not-touch files (if any)
- Suggested first action for next session
```

**Format:** Fill all bracketed placeholders. Remove stale entries from previous sessions.

---

### CURRENT_FOCUS.md

**Purpose:** Keeps any agent aligned with what is actively being worked on right now.

**When to update:**
- When a task moves to `in-progress` → update to reflect new task
- When a task moves to `done` or `review` → clear the active task field
- When the active epic changes → update epic and goal fields
- When the human redirects the work mid-session

**Who updates it:** Orchestrator agent as part of the task transition AI layer update proposal.

**Trigger phrase in proposal:**
```
Brain
- CURRENT_FOCUS.md → set active task to TASK_xxx, epic EPIC_yyy
```

**Do not leave stale:** If no task is active, the file must say `none` — not the previous task.

---

### PROJECT_STATE.md

**Purpose:** Snapshot of what is currently working, what is broken, and what the immediate technical goal is.

**When to update:**
- After every task is completed (sub-agent updates this as part of its post-task proposal)
- After a spike task resolves a technical uncertainty
- After a build or test failure that changes the health status of a system
- At the start of a new epic (to confirm baseline state)

**Who updates it:** Sub-agent proposes updates after task completion. Orchestrator updates at epic transitions.

**What to include:**
- Systems confirmed working (with last verified date or task ID)
- Systems known broken or incomplete
- Current technical goal (one sentence)
- Blocked items (with reason and blocking dependency)

**Do not include:** Task history, decisions, next steps — those belong in other brain files.

---

### DECISIONS_LOG.md

**Purpose:** Permanent record of confirmed decisions so agents never re-litigate settled questions.

**When to update:**
- When an open question in `OPEN_QUESTIONS.md` is resolved → move the answer here
- When a significant architectural or design decision is made during spec authoring
- When a spike task concludes with a confirmed direction
- When the human explicitly overrides a proposed approach

**Who updates it:** Orchestrator agent. The decision must be proposed in the AI layer update before being written.

**Format per entry:**
```
- [YYYY-MM-DD] [DECISION_ID or TASK_ID] — [decision statement] — [rationale in one sentence]
```

**Do not include:** Tentative ideas, open questions, or implementation details better suited to memory files.
**Do not delete** entries — append only. Mark superseded decisions with `[superseded by DECISION_ID]`.

---

### NEXT_STEPS.md

**Purpose:** Ordered list of the next concrete actions the orchestrator should take.

**When to update:**
- After every task transition (remove completed item, add next item)
- After spec approval (populate with epic breakdown steps)
- When a blocker is discovered (add "unblock X before proceeding")
- At session start if the list is stale (older than one session)

**Who updates it:** Orchestrator agent as part of every task transition proposal.

**Format:** Numbered list, ordered by priority. Each item must be actionable in one step.
```
1. [Concrete next action] — [reason / context]
2. ...
```

**Prune aggressively:** Remove items that are done. Keep the list to 5–7 items maximum.
If there are more than 7 items, consolidate or move lower-priority items to `OPEN_QUESTIONS.md`.

---

### OPEN_QUESTIONS.md

**Purpose:** Backlog of unresolved questions that are known but not blocking current work.

**When to add a question:**
- During spec co-authoring when a gap is found but cannot be resolved immediately
- During architecture review when a spike is not yet scheduled
- During task execution when something unexpected is discovered
- Any time a decision is deferred

**When to remove a question:**
- When it is resolved → move the answer to `DECISIONS_LOG.md`
- When it is determined to be irrelevant → delete with a note in the proposal

**Who updates it:** Any agent may propose additions. Removal requires a corresponding entry in `DECISIONS_LOG.md`.

**Format per entry:**
```
- [ ] [Question] — [why it matters] — [blocking: yes/no] — [added: TASK_ID or date]
- [x] [Resolved question] — [resolution summary] → see DECISIONS_LOG [DECISION_ID]
```

---

## Brain Consistency Check

At the start of every orchestrator session, verify:

| Check | Expected state |
|-------|---------------|
| `SESSION_HANDOFF.md` active task matches `CURRENT_FOCUS.md` | Same TASK_ID |
| `CURRENT_FOCUS.md` task exists in `TASK_INDEX.md` as `in-progress` | Task present |
| `NEXT_STEPS.md` top item is actionable right now | Not blocked |
| `OPEN_QUESTIONS.md` has no resolved questions still marked `[ ]` | All resolved marked `[x]` |

If inconsistencies are found → propose a sync update before starting any task work.

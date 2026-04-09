# Memory Governance

This document defines how memory files are created, updated, versioned, and deprecated.

Memory files hold **durable knowledge** — patterns, rules, and lessons that remain true
across sessions, tasks, and epics. Unlike brain files (which change often), memory files
change rarely and deliberately.

---

## The Four Memory Files and Their Purpose

| File | Holds | Changes when |
|------|-------|-------------|
| `DOMAIN_RULES.md` | Business / domain rules that must always be respected | Domain understanding changes |
| `CONTENT_CONVENTIONS.md` | Naming, file structure, and formatting conventions | A new convention is agreed upon |
| `TECHNICAL_PATTERNS.md` | Accepted code patterns and architectural preferences | A pattern is proven or disproven by experience |
| `KNOWN_PITFALLS.md` | Things that have gone wrong or are likely to go wrong | A new failure mode is discovered |

---

## Who Can Update Memory Files

| Role | May propose | May apply |
|------|-------------|-----------|
| Orchestrator agent | Yes | Only after human `Yes` |
| Sub-agent | Yes (pitfalls and patterns only) | Only after human `Yes` |
| Human | Yes | Directly, at any time |

Memory updates must be included in the standard AI layer update proposal.
Memory files are **never modified silently**.

---

## File-by-File Rules

---

### DOMAIN_RULES.md

**Purpose:** Rules derived from business or product understanding that agents must never violate.
Example: "A user account can only belong to one organisation at a time."

**When to add a rule:**
- When a spec or architecture review reveals a domain constraint that must always be respected
- When a sub-agent violates a domain rule and the violation is caught — add the rule to prevent recurrence
- When the human explicitly states a rule during co-authoring

**When to update or remove a rule:**
- When the domain changes (e.g. product pivot) — update with a note: `[updated YYYY-MM-DD: reason]`
- When a rule is found to be incorrect — mark as `[deprecated YYYY-MM-DD: reason]`, do not delete

**Who updates it:** Orchestrator agent proposes, human approves. Never updated by a sub-agent alone.

**Format per rule:**
```
- [Rule statement in plain language.] [Source: SPEC_ID or decision date]
- [deprecated YYYY-MM-DD: reason] [old rule]
```

---

### CONTENT_CONVENTIONS.md

**Purpose:** Naming conventions, folder structure rules, and formatting standards that all agents must follow.

**When to add a convention:**
- When a new repository or framework is added to scope and its conventions are established
- When a naming conflict arises during a task and a decision is made to resolve it
- When the human specifies a preference that should be consistent across the project

**When to update:**
- When a convention is changed project-wide — update the entry and add `[changed YYYY-MM-DD: from X to Y]`
- When a convention is retired — mark `[deprecated YYYY-MM-DD]`, do not delete

**Who updates it:** Orchestrator agent proposes, human approves.

**Format:**
```
## [Repository or scope name]

Naming:
- [pattern]: [example]

Structure:
- [rule]

Deprecated:
- [deprecated YYYY-MM-DD] [old convention]
```

---

### TECHNICAL_PATTERNS.md

**Purpose:** Accepted implementation patterns that sub-agents should follow by default.

**When to add a pattern:**
- When a spike task confirms a specific approach works well
- When the same solution is used successfully in 2+ tasks — it is ready to be a pattern
- When the human explicitly mandates an approach

**When to update or remove:**
- When a pattern is proven wrong by a failing task → mark `[deprecated YYYY-MM-DD: reason]`
- When a better pattern supersedes an old one → add the new one and deprecate the old

**Who updates it:**
- Sub-agents may **propose** additions based on task experience
- Orchestrator reviews and approves proposals
- Human has final say on all changes

**Format:**
```
## [Pattern name]
Context: [when this applies]
Pattern: [what to do]
Rationale: [why this was chosen over alternatives]
Source: [TASK_ID or SPEC_ID that established this]
Status: active | deprecated [YYYY-MM-DD: reason]
```

---

### KNOWN_PITFALLS.md

**Purpose:** A catalogue of failure modes, gotchas, and mistakes that have occurred or are predictable.

**When to add:**
- Immediately after a sub-agent task fails due to a non-obvious reason
- When a harness bootstrap reveals a platform-specific issue
- When a metaharness run identifies a recurring failure pattern
- When the human warns the team about a known issue in the stack

**When to resolve or retire:**
- When the root cause is fixed permanently → move the entry to an `[archived]` section with the fix reference
- When the pitfall no longer applies (e.g. library version bump) → mark `[resolved YYYY-MM-DD: reason]`

**Who updates it:** Any agent may propose. Orchestrator batches proposals into the AI layer update.

**Format:**
```
- [Pitfall description.] [Stack or context where it applies.] [Workaround: ...] [Source: TASK_ID]
- [resolved YYYY-MM-DD] [old pitfall] → fixed by [TASK_ID or change]
```

---

## Memory Promotion Process

Not every observation belongs in memory immediately. Use this ladder:

```
Task notes (ephemeral, in the task file)
  → Proposed in AI layer update (reviewed)
    → Added to memory file (after approval)
      → Reviewed after 3+ confirming instances (pattern/rule solidified)
        → Deprecated when superseded
```

A sub-agent should **not** write directly to memory files. It should include the proposed addition
in its post-task AI layer update proposal under the `Memory` section:

```
Memory
- KNOWN_PITFALLS.md: add pitfall — [description] — Source: TASK_xxx
- TECHNICAL_PATTERNS.md: add pattern — [name] — Source: TASK_xxx
```

---

## Memory Consistency Check

At the start of each new epic, the orchestrator should verify:

| Check | Action |
|-------|--------|
| Any pitfall in `KNOWN_PITFALLS.md` directly relevant to this epic's stack? | Surface it in the sub-agent's task briefing |
| Any technical pattern that should guide task implementation? | Reference it in the task's `## Constraints` section |
| Any domain rule that constrains the epic's scope? | Confirm it is reflected in the epic's `## Out of Scope` section |
| Any deprecated rule still referenced in spec or task files? | Propose an update to remove the stale reference |

# Rules Evolution

This document governs how the operating layer's **rule files** can be proposed, reviewed, and changed.

Rule files are different from state files (brain) and knowledge files (memory).
They define **how the system operates** — changing them changes the behaviour of every future agent.

---

## Which Files Are Rule Files

| File | Locked by default | Can be changed by |
|------|-------------------|-------------------|
| `agent/AGENTS.md` | Yes (Tier 3) | Human explicit instruction only |
| `epics/EPIC_SELECTION_RULES.md` | Soft lock | Proposal + human `Yes` |
| `tasks/TASK_SELECTION_RULES.md` | Soft lock | Proposal + human `Yes` |
| `metaharness/HARNESS_RULES.md` | Yes (Tier 3) | Human explicit instruction only |
| `metaharness/HARNESS_UPDATE_PROTOCOL.md` | Yes (Tier 3) | Human explicit instruction only |
| `agents/HARNESS_BOOTSTRAP.md` | Yes (Tier 3) | Human explicit instruction only |
| `brain/BRAIN_UPDATE_PROTOCOL.md` | Soft lock | Proposal + human `Yes` |
| `memory/MEMORY_GOVERNANCE.md` | Soft lock | Proposal + human `Yes` |
| `architecture/RULES_EVOLUTION.md` | Yes (Tier 3) | Human explicit instruction only |
| `specs/SPEC_WORKFLOW.md` | Soft lock | Proposal + human `Yes` |

**Tier 3 (hard lock):** These files define the rules of the system itself. No agent may modify them
without explicit human instruction in the conversation. They are never included in a routine
AI layer update proposal.

**Soft lock:** These files can evolve as the project matures, but only through a formal proposal.

---

## How To Propose A Rule Change

Any agent or human may propose a change to a soft-locked rule file.

### Proposal Format

```
Proposed rule change:

File: .ai/[path/to/rule-file].md
Section: [section heading]
Reason: [why the current rule is not working or needs refinement]
Evidence: [task, epic, or session that revealed the gap — be specific]

Change:
  - old: [current rule text]
  + new: [proposed rule text]

Impact: [what behaviour changes if this is approved]
Risk: [what could go wrong if the change is wrong]

Approve rule change? (Yes / No)
```

### Who Can Propose

- **Orchestrator agent:** may propose changes to selection rules and workflow files
- **Sub-agent:** may NOT propose rule changes — it must flag the issue to the orchestrator
- **Human:** may propose at any time, directly in conversation

### Review Criteria

Before approving a rule change, consider:

1. Is there evidence from at least one real task or session that the current rule caused a problem?
2. Does the proposed rule generalise — or is it a special case better handled in a task?
3. Does the change conflict with any Tier 3 rule?
4. Would this change make future agents more or less predictable?

---

## ARCHITECTURE_DECISIONS.md Governance

`architecture/ARCHITECTURE_DECISIONS.md` records primary technical decisions (stack, framework, patterns).
These are not selection rules but they are similarly sensitive.

**When to update:**
- When a new repository is added to scope and its stack is confirmed
- When a spike task results in a confirmed engine or framework choice
- When a previously assumed decision turns out to be wrong

**Format per decision:**
```
## Decision: [short name]
Date: YYYY-MM-DD
Status: active | superseded [by: decision name, date]
Context: [what question this answers]
Decision: [what was decided]
Rationale: [why this, not the alternatives]
Consequences: [what this rules in or out going forward]
```

**Who updates it:** Orchestrator agent proposes, human approves.
Old decisions must never be deleted — set `Status: superseded` and add the replacement.

---

## Rule Stability Principle

Rules should be **stable by default and changed only under evidence**.

If a rule is being proposed for change more than once per epic, that is a signal that
the rule is too prescriptive or the wrong abstraction — consider removing the rule entirely
rather than iterating on its wording.

The fewer rules there are, the more reliably agents follow them.

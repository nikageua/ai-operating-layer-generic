# Architecture Decisions

This file records confirmed cross-cutting technical decisions that apply across
all repositories and frameworks in scope.

These are not preferences or guidelines — they are resolved choices that sub-agents
must treat as constraints. Do not re-litigate them in tasks or specs unless a
formal decision revision is proposed (see `RULES_EVOLUTION.md`).

---

## How To Read This File

Each decision follows this format:

```
## Decision: [short name]
Date: YYYY-MM-DD
Status: active | superseded [by: decision name, date]
Context: [what question this resolves]
Decision: [what was decided]
Rationale: [why this, not the alternatives]
Consequences: [what this rules in or out going forward]
```

Decisions are append-only. Superseded decisions are marked but never deleted.

---

## Decision: [placeholder — fill in your first decision]

Date: YYYY-MM-DD
Status: active

Context:
[What architectural question needed to be resolved? e.g. "How do services communicate across repositories?"]

Decision:
[What was decided? e.g. "All cross-service communication uses REST over HTTP with JSON. No direct database sharing between services."]

Rationale:
[Why this choice? e.g. "Team is already familiar with REST; gRPC adds operational complexity that is not justified at current scale."]

Consequences:
- [What is now ruled in] e.g. Each service owns its own database schema.
- [What is now ruled out] e.g. Shared database tables across services are not permitted.
- [What must be true going forward] e.g. New services must expose a REST API before any consumer can integrate.

---

## Anti-Scope-Creep Rule

Do not introduce cross-cutting decisions into this file during task execution.
Architecture decisions emerge from:
1. Spec authoring (when cross-repo constraints are identified)
2. Spike tasks (when a technical question must be resolved before implementation)
3. Epic review (when a pattern proven in one epic should become a constraint for all)

If a sub-agent discovers an architectural inconsistency during a task,
it must flag it in `OPEN_QUESTIONS.md` and pause — not resolve it unilaterally.

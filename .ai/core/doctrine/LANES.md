# Execution Lanes

AIL v2 uses three execution lanes so that small work stays light and risky work still gets structure.

## Why lanes exist

A major failure mode in AI-assisted delivery is using one heavy process for every kind of task.
That creates bureaucracy for small work and bypass behavior for real teams.

Lanes solve that by making process depth proportional to risk, scope, and uncertainty.

---

## Tiny

Use Tiny when the work is narrow, local, and low-risk.

Typical examples:
- small bugfix in one known file
- rename or wording cleanup
- low-risk UI tweak
- safe refactor with clear blast radius
- small test fix

Required artifacts:
- task only

Optional artifacts:
- architecture sanity note, only if a boundary or hidden risk exists
- runtime attempt note, only if blocked

Tiny is the default when you are strongly tempted to say:
- "this should take one session"
- "I already know where this belongs"
- "this does not change ownership or architecture"

### Tiny anti-patterns
Do not use Tiny when:
- the change spans multiple repos
- the correct ownership is unclear
- you are changing contracts or boundaries
- you expect likely retries because the shape of the problem is uncertain
- the task contains multiple distinct deliverables hidden under one label

If any of those are true, escalate to Standard.

---

## Standard

Use Standard for regular feature work or medium-complexity changes where some structure helps but full heavyweight planning would be wasteful.

Typical examples:
- feature addition in one repo
- one or two predictable repo changes with clear ownership
- backend endpoint plus matching frontend consumption when the contract is straightforward
- moderate refactor where the destination structure is known

Required artifacts:
- task
- light spec when it clarifies the work
- architecture sanity check

Use Standard when:
- implementation is not fully trivial
- there is more than one reasonable design choice
- the change touches behavior, not just syntax
- future maintenance could get worse if placement is wrong

### Standard anti-patterns
Do not use Standard when:
- the work changes core boundaries or multiple major repos
- requirements are still fuzzy
- the right abstraction is unknown
- the change is risky enough that rework would be expensive

If those are true, escalate to Architectural.

---

## Architectural

Use Architectural for work where the cost of getting structure wrong is high.

Typical examples:
- cross-repo feature with contract changes
- auth, identity, billing, permissions, shared state, or infrastructure changes
- significant refactor with uncertain landing zone
- changes where architecture debt is likely if done as isolated local edits
- work requiring spikes before implementation

Required artifacts:
- light spec
- architecture sanity check
- story or task breakdown
- explicit trade-off and risk note

Architectural is not a badge of importance. It is a lane for managing uncertainty and blast radius.

---

## Decision matrix

Choose based on these four questions:

1. **Scope:** Is the work local or cross-cutting?
2. **Risk:** If we place it wrong, is cleanup cheap or expensive?
3. **Uncertainty:** Do we know the shape of the solution already?
4. **Coordination:** Does more than one repo, agent, or developer need the same framing?

Rule of thumb:
- low scope + low risk + low uncertainty → Tiny
- moderate scope or uncertainty → Standard
- high risk, high uncertainty, or cross-repo coordination → Architectural

---

## Escalation rules

A task must move to a higher lane when:
- two failed attempts happen without convergence
- hidden boundary changes appear
- more repos become involved than initially assumed
- the "simple" task actually contains multiple distinct deliverables
- a supposedly local fix reveals architectural coupling

The lane is not sacred. Changing lanes is healthy when new evidence appears.

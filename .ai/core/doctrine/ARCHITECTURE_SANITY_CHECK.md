# Architecture Sanity Check

This check exists to force one short structural pause before non-trivial implementation.
It is not a spec. It is a guardrail against local AI edits creating global design debt.

Use for Standard and Architectural lane work.

---

## The 5 questions

1. **Where should this logic live?**
   Name the repo, layer, or component where the logic belongs.

2. **Which component or layer owns it?**
   Identify the owner, not just the file you happen to be touching.

3. **Which boundary must not be crossed?**
   State the main separation that should stay intact.

4. **What trade-off is being chosen?**
   Every design choice pays somewhere. Make the payment explicit.

5. **What is the main maintenance, security, or scaling risk?**
   Name the main future pain you are trying not to create.

---

## Good answer example

- location: `repo:identity-api`, authentication service layer
- owner: backend auth boundary
- boundary: frontend must not implement token refresh rules directly
- trade-off: one extra backend change now to keep auth logic centralized
- risk: session bugs if refresh edge cases are not regression-tested

Why this is good:
- it names ownership,
- it protects a boundary,
- it acknowledges the trade-off,
- it identifies the real future risk.

---

## Weak answer example

- location: wherever easiest
- owner: current task
- boundary: none
- trade-off: speed
- risk: maybe bugs

Why this is weak:
- no ownership,
- no system boundary,
- no concrete risk,
- no structural reasoning.

---

## Common smells

If you notice one of these, stop and rethink placement:
- UI starts carrying business rules
- backend starts depending on frontend-specific state shape
- shared modules become dumping grounds
- the easiest location is not the rightful owner
- one task quietly changes a contract that other repos rely on

---

## Rule of use

Keep this short.
If the answer becomes long, that is usually a sign you actually need a spec or spike.


## Loading model

- Tiny: do not load architectural decisions by default.
- Standard: load `ARCHITECTURAL_CONSTRAINTS.md`, then pull relevant decision notes only if triggered.
- Architectural: load `ARCHITECTURAL_CONSTRAINTS.md`, relevant decision notes, and the current story/spec architecture note.

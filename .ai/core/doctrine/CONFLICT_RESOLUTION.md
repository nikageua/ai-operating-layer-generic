# Conflict Resolution

AIL v2 needs a way to resolve contradictory learnings before they become shared truth.

## Common conflict types
- two stories suggest different "best" patterns
- one lesson is reusable, another is just a local exception
- two proposals target the same durable doc with different wording
- a lesson is valid only for one repo or one stack slice

## Resolution options

### Narrow scope
If a lesson is only valid for one repo or one context, keep it scoped there.
Do not promote it as project-wide truth.

### Split truth
If both conclusions are valid in different contexts, encode the distinction explicitly instead of forcing one false universal rule.

### Defer promotion
If evidence is still weak or contradictory, keep the lesson in runtime or story-local space until more signal appears.

### Reject
If a proposal adds more noise than decision value, reject it.

## Curator responsibility

The main curator must resolve contradictory updates before promotion.
Durable docs should not become the place where unresolved debate is stored as pseudo-truth.

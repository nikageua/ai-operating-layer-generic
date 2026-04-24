# Example: Failed task recovery

## Scenario
A task starts as a Standard change: add silent token refresh for an existing frontend session flow.
The first attempt implements refresh behavior directly in the frontend session manager.
The second attempt patches another UI-side workaround after integration problems appear.

At this point the task is failing, not because of syntax mistakes, but because the shape is wrong.

## Attempt 1

```md
- approach: implement token refresh directly in frontend session state
- result: failed
- failure-class: wrong-abstraction
- evidence: refresh rules depend on backend token lifecycle the UI does not own
- next-step: move logic review to auth boundary
```

## Attempt 2

```md
- approach: patch frontend around expired-token edge case
- result: failed
- failure-class: architecture-unclear
- evidence: session behavior depends on hidden backend refresh semantics
- next-step: create spike for token ownership and refresh contract
```

## What the system should do now
After two failed attempts, AIL should not allow "try again but harder".
It should force at least one meaningful change, such as:
- split task,
- create spike,
- revise architecture note,
- move lane upward,
- update profile/overlay guidance.

## Correct recovery move
In this case, the right next move is:
- escalate from Standard to Architectural,
- create a spike around refresh-token ownership,
- write a durable pitfall only if the lesson is reusable.

## Common mistake
Logging failure without changing behavior.
That creates the illusion of learning while repeating the same structural error.

## Durable promotion rule
Do not immediately write this into project doctrine unless:
- similar auth-boundary mistakes repeated,
- or the incident exposed a broadly reusable rule.
Otherwise keep it as runtime learning only.

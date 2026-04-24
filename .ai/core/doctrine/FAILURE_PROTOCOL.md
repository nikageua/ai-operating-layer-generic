# Failure Protocol

AIL v2 treats failure handling as a first-class part of delivery.
The goal is not to log that something failed. The goal is to avoid repeating the same bad move.

---

## Principle

A failed attempt should change one of these:
- the understanding of the problem,
- the framing of the task,
- the design approach,
- the required context,
- the chosen validation path.

If nothing changes after failure, the system is not learning.

---

## Failure classes

### implementation-gap
The task is valid, but the chosen implementation was incorrect or incomplete.

Signals:
- compile/test failures from a plausible approach
- the design is still sound, but execution was flawed

Typical next move:
- retry-with-new-approach

### task-too-large
The task bundled too much change into one unit.

Signals:
- multiple unrelated blockers
- progress in one area creates ambiguity in another
- acceptance is too broad for one session

Typical next move:
- split-task

### wrong-abstraction
The chosen design shape is itself the problem.

Signals:
- code can be made to work, but ownership feels wrong
- logic wants to live elsewhere
- duplication or coupling increases sharply

Typical next move:
- revise-architecture-note
- create-spike

### architecture-unclear
The team or agent does not yet know the right structural placement.

Signals:
- more than one plausible owner
- boundary questions dominate implementation questions
- local fixes keep leaking across layers

Typical next move:
- create-spike
- revise-spec
- revise-architecture-note

### repo-context-missing
The agent lacks enough repo-specific knowledge to act safely.

Signals:
- conventions are unclear
- commands, folder intent, or integration patterns are not known
- agent keeps rediscovering basic local rules

Typical next move:
- update-profile-or-overlay

### harness-profile-mismatch
The selected profile does not fit the real work.

Signals:
- validation steps are wrong
- stack assumptions do not match touched code
- profile advice keeps pulling implementation in the wrong direction

Typical next move:
- update-profile-or-overlay

### environment-blocked
The problem is caused by local environment, unavailable services, secrets, or test setup.

Signals:
- code changes are blocked by runtime setup
- app cannot start, connect, or validate locally

Typical next move:
- mark-blocked-with-evidence
- update local runtime mapping or setup

### external-dependency-blocked
Another team, service, contract, or system is blocking progress.

Signals:
- waiting on a real outside dependency
- implementation is constrained by something not under local control

Typical next move:
- mark-blocked-with-evidence

---

## Allowed next transitions

- retry-with-new-approach
- split-task
- create-spike
- revise-architecture-note
- revise-spec
- update-profile-or-overlay
- mark-blocked-with-evidence

---

## Distinguishing common confusions

### task-too-large vs wrong-abstraction
- **task-too-large**: the work is too broad, but the overall design still makes sense
- **wrong-abstraction**: even a smaller version of this task would still be shaped badly

### implementation-gap vs architecture-unclear
- **implementation-gap**: you know where the logic should live, but failed to implement it correctly
- **architecture-unclear**: you are not yet confident where the logic belongs at all

### repo-context-missing vs environment-blocked
- **repo-context-missing**: knowledge problem
- **environment-blocked**: runtime/setup problem

---

## Escalation rule

After 2 failed attempts, do not repeat the same task shape without reclassification.

That means at least one of the following must change:
- failure class
- lane
- task breakdown
- architecture note
- profile or overlay guidance
- validation strategy

---

## Attempt note shape

When an attempt is worth recording in `.ai/runtime/attempts/`, keep it short and structured:

```md
## Attempt 2
- approach: direct integration into auth pipeline
- result: failed
- failure-class: architecture-unclear
- evidence: hidden dependency on legacy token refresh flow
- next-step: create spike for auth boundary mapping
```

Record only when useful. Happy-path work should not create paperwork.

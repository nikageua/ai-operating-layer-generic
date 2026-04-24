# Update Governance

AIL v2 is designed to evolve semi-automatically.
That means runtime learning can happen quickly, but durable shared truth must change slowly and intentionally.

This file defines who may change what, when proposals are required, and how hooks should enforce those rules.

---

## Governance goals

1. Prevent sub-agents from mutating durable AIL truth directly.
2. Preserve a learning loop without turning every lesson into bureaucracy.
3. Keep runtime experimentation fast.
4. Route durable changes through a main-agent curation step.
5. Require human approval for meaningful shared AIL updates.

---

## Authority model

### Sub-agent
May:
- read all AIL files
- write local runtime notes
- write attempt notes
- create candidate update proposals in runtime proposal space

May not:
- directly modify durable files in `.ai/core/`
- directly modify durable files in `.ai/project/`

### Main / orchestrator agent
May:
- read all AIL files
- curate proposed updates
- decide whether a candidate is worth promotion
- prepare durable AIL updates
- ask the human for approval

May not:
- silently mutate durable AIL without the defined approval path

### Human
Approves durable changes to shared truth.
The human is the final authority for changes that alter project doctrine, project memory, or core behavior.

---

## File classes

### Class R — Runtime local
Examples:
- `.ai/runtime/local-map.yaml`
- `.ai/runtime/attempts/*`
- `.ai/runtime/active/*`
- `.ai/runtime/proposed-updates/*`

Properties:
- local or volatile
- not durable shared truth
- sub-agents may write here

Approval:
- no human approval required by default

### Class P — Project durable
Examples:
- `.ai/project/KNOWN_PITFALLS.md`
- `.ai/project/TECHNICAL_PATTERNS.md`
- `.ai/project/CONVENTIONS.md`
- `.ai/project/ARCHITECTURAL_CONSTRAINTS.md`
- `.ai/project/AGENT_PROFILES/*`
- tracked story/spec/task artifacts

Properties:
- shareable project truth
- medium blast radius
- evolves from repeated learnings or clarified conventions

Approval:
- main agent proposal required
- human approval required before durable update

### Class C — Core durable
Examples:
- `.ai/core/LANES.md`
- `.ai/core/FAILURE_PROTOCOL.md`
- templates
- governance rules
- migration docs
- `INIT_PROMPT.md`

Properties:
- framework-level truth
- highest blast radius
- affects future behavior broadly

Approval:
- main agent proposal required
- explicit human approval required
- stronger scrutiny than Class P

---

## When to propose an update

A durable update proposal should be created when at least one is true:
- a lesson repeated 2 or more times
- an expensive failure exposed a reusable truth
- a structural ambiguity was resolved in a reusable way
- a project convention had to be rediscovered multiple times
- a profile repeatedly guided work badly
- a template or protocol proved insufficient in a recurring way

Do not propose a durable update when:
- the lesson is purely local or temporary
- the issue is a one-off environment problem
- the note has no reuse value
- the change would just document noise

---

## Proposal flow

### Step 1: Candidate capture
A sub-agent or main agent may create a candidate in:
- `.ai/runtime/proposed-updates/`

### Step 2: Main-agent curation
The main agent reviews the candidate and decides:
- discard
- keep local only
- promote to project-level proposal
- promote to core-level proposal

### Step 3: Human approval
Before modifying Class P or Class C durable files, the main agent must show a proposal and ask for approval.

### Step 4: Durable update
Only after approval may the durable AIL update be applied.

---

## Required proposal format

```md
# Proposed AIL Update

## Scope
- core | project

## Reason
- what was learned
- why it matters now
- what future mistake or ambiguity this prevents

## Changes
- file: ...
  action: create | update | archive
  summary: ...

## Source evidence
- attempt / story / task / incident reference

## Approval required
- yes
```

---

## Hook contract

Hooks are the enforcement layer for this governance model.
They should prevent invalid durable writes and route candidate learnings into the right place.

Hooks should enforce at least these rules:

1. **Sub-agent durable write barrier**
   - if actor is a sub-agent and target is `.ai/core/**` or `.ai/project/**`
   - block direct write
   - instruct the agent to create a candidate proposal in runtime instead

2. **Durable update approval barrier**
   - if target is `.ai/project/**` or `.ai/core/**`
   - require proof that main-agent approval flow is being followed

3. **Local-env leakage barrier**
   - warn or block if tracked files contain:
     - absolute local paths
     - machine-specific localhost URLs as shared truth
     - other machine-specific environment details

4. **Noise control**
   - warn if durable updates have no reason/evidence structure
   - discourage creating durable docs with no clear reuse value

---

## Semi-automatic philosophy

AIL should learn automatically at runtime level,
but durable truth should change only through:
- candidate capture,
- curation,
- approval,
- and intentional promotion.

That is what "semi-automatic" means in AIL v2.

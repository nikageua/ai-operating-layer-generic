# Hooks Spec

This file describes the intended hooks behavior for AIL v2.
It is a contract, not an implementation.

---

## Purpose

Hooks should act as lightweight enforcement for update governance.
They should not replace human judgment or operating doctrine.
They should prevent invalid mutations and route learning into the right channel.

---

## Hook targets

### Target 1: Durable write attempts
If an actor tries to modify:
- `.ai/core/**`
- `.ai/project/**`

Then the hook should inspect:
- actor role
- whether the update is direct or proposal-driven
- whether required approval markers exist

### Target 2: Runtime writes
If an actor writes to:
- `.ai/runtime/**`

The hook should usually allow it, unless the write violates basic hygiene or naming rules.

### Target 3: Tracked content hygiene
For tracked files, hooks should scan for:
- absolute local paths
- workstation-specific URLs
- obvious machine-local state leakage

---

## Actor-aware behavior

### Sub-agent
- allow writes to runtime
- block direct writes to durable AIL files
- suggest runtime proposal capture instead

### Main agent
- allow runtime writes
- allow proposal preparation
- require approval workflow for durable changes

### Human-approved path
- allow durable changes once approval gate is satisfied

---

## Suggested enforcement outcomes

### Block
Use when:
- sub-agent tries to mutate durable files directly
- local machine detail is being committed into shared truth

### Warn
Use when:
- a durable update lacks enough reason/evidence structure
- a new doc is being added with weak justification

### Reroute
Use when:
- a sub-agent has a useful lesson but no durable authority
- convert the action into a candidate proposal flow

---

## Minimal hook messages

Good hook messages are short and actionable.

Examples:
- "Direct write to `.ai/project/**` blocked for sub-agent. Create a candidate in `.ai/runtime/proposed-updates/` instead."
- "Tracked file contains an absolute local path. Replace it with a logical repo or env ID."
- "Durable update lacks proposal structure. Add scope, reason, evidence, and target files."

---

## Non-goals

Hooks should not:
- act as a replacement for architecture thinking
- auto-promote runtime notes into durable truth without curation
- create large volumes of process noise
- silently rewrite project doctrine

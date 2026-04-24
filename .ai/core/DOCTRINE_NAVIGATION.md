# Doctrine Navigation

AIL v2 doctrine is pull-based, not all-at-once.
Do not read every doctrine file for every session.

## Tier 0 — Usually read
Read these in most sessions:
- `README.md`
- `doctrine/LANES.md`
- `doctrine/FAILURE_PROTOCOL.md`
- `doctrine/UPDATE_GOVERNANCE.md`

## Tier 1 — Read when triggered
Read only when the work requires it:

- `doctrine/ARCHITECTURE_SANITY_CHECK.md`
  - when lane is Standard or Architectural
  - when ownership or placement is unclear

- `doctrine/CROSS_REPO_IMPACT.md`
  - when more than one repo is touched or suspected

- `doctrine/KNOWLEDGE_SCOPES.md`
  - when deciding whether a lesson is local or shared

- `doctrine/CONFLICT_RESOLUTION.md`
  - when multiple candidate truths conflict

- `doctrine/PARALLEL_WORK_MODEL.md`
  - when multiple stories or sessions are active in parallel

- `doctrine/RUNTIME_LIFECYCLE.md`
  - when runtime accumulation, cleanup, or retention becomes relevant

- `references/NAMING_AND_IDS.md`
  - when creating new story/task/spec/spike/proposal files

## Tier 2 — Curator / maintenance only
Read occasionally, not by default:
- `doctrine/OWNERSHIP_MODEL.md`
- `doctrine/OPERATING_LAYER_HEALTH.md`
- `doctrine/ANTI_BLOAT.md`
- `doctrine/ADOPTION_PATH.md`
- `references/HOOKS_SPEC.md`
- `references/PROMOTION_RULES.md`
- `migrations/*`

## Rule
If a file does not change the next decision, do not load it.

- `doctrine/REVERSIBILITY.md`
  - when a change looks small but may be hard to undo
- `doctrine/STOP_AND_ASK.md`
  - when irreversible or expanding work needs human alignment
- `doctrine/CONTEXT_BUDGET.md`
  - when token usage or loading discipline matters

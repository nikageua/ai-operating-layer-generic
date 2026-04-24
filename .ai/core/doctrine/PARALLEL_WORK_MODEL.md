# Parallel Work Model

AIL v2 must support multiple developers and AI sessions working in parallel on different stories without corrupting shared truth.

## Unit of parallel work

The primary unit of parallel coordination is the **story**.

Why:
- a task is often too small and ephemeral to serve as the main coordination surface,
- a branch is a VCS unit, not an operating doctrine unit,
- a spike is a special-purpose investigative artifact, not the default concurrency container.

Use tasks inside a story.
Use spikes inside a story when uncertainty demands them.

## Isolation model

Each active story should have its own local or shared coordination surface.
Story-local conclusions should not become project truth automatically.

### Story-local knowledge
Lives with the story and explains:
- assumptions,
- intermediate findings,
- temporary decisions,
- local experiments,
- unresolved ambiguity.

### Shared project knowledge
Only promote a story-local lesson when it is proven reusable beyond that one story.

## Parallel sessions rule

Multiple sessions may work in parallel if:
- each session has a clear story or task scope,
- their runtime notes stay isolated,
- they do not directly mutate shared durable truth without curation.

## Parallel candidate updates

If multiple stories produce candidate updates touching the same durable file:
- do not auto-merge them into shared truth,
- queue them as separate proposals,
- let the main curator resolve overlap before promotion.

## Good parallel shape

- story as coordination unit
- task as execution unit
- runtime as local scratch and attempt memory
- project/core as curated truth only

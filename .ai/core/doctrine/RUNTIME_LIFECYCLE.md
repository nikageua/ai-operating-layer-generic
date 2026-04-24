# Runtime Lifecycle

The runtime layer exists for volatile, local, and fast-moving context.
It must stay useful without becoming a graveyard.

## Runtime scope

By default, runtime is per local workspace / machine context.
Within runtime, notes may be organized per story or per active session when useful.

## Typical runtime contents
- local path and env mapping
- attempt notes
- local scratch notes
- candidate durable update proposals

## Retention guidance

### Keep longer
- attempt notes that still inform an active story
- candidate proposals awaiting curation
- runtime notes tied to ongoing work

### Archive or drop
- abandoned local experiments with no reuse value
- stale active-session notes after the story is closed
- proposals already accepted, rejected, or superseded

## Hygiene rule

If a runtime note no longer changes a future decision, archive or delete it.

## Suggested cleanup cadence
- cleanup lightweight runtime debris when closing a story
- review stale proposals periodically
- do not let runtime become a shadow knowledge base

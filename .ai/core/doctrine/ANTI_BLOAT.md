# Anti-Bloat Doctrine

Every operating layer tends to grow unless it has explicit rules against useless expansion.

## Hard rules

- do not create a durable doc without repeatable decision value
- do not promote local noise into shared truth
- do not create story/spec/task artifacts without real coordination value
- if a document does not change future decisions, it does not deserve durable status

## Smells
- a new file exists only because the structure had an empty slot
- the same truth is repeated in multiple places
- a story-local workaround becomes project doctrine after one incident
- templates are created but not used
- docs are updated to satisfy ritual rather than improve future work

## Pruning principle

A smaller high-signal overlay is better than a large polite archive of forgotten context.

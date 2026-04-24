# Example: Parallel multi-story work

## Scenario
Dev A works on a resend-confirmation flow.
Dev B works on an invite-user flow.
Both touch `repo:identity-api`, but only one lesson should become shared truth.

## Correct behavior
- each story keeps local notes and attempts separate
- both may create runtime candidate proposals
- main curator reviews overlap before promotion
- only reusable identity-boundary lessons become project truth
- story-specific noise stays local

## What this protects
- prevents premature shared-memory pollution
- keeps parallel work from colliding in durable docs
- forces curation instead of accidental doctrine drift

# Example: Architectural story

## Scenario
The product needs a user invite flow where:
- an admin invites a user from the frontend,
- the identity backend creates an invitation token,
- an email component sends the invite,
- the invited user completes onboarding through a separate route,
- audit or permission logic must remain consistent.

This spans multiple repos and touches security-sensitive flows.

## Why this is Architectural
- cross-repo
- contract-heavy
- identity and permission boundaries matter
- one wrong local shortcut could create long-lived design debt
- sequencing and ownership are more important than raw coding speed

## Required artifacts
- story
- light spec
- architecture sanity check
- task breakdown
- explicit trade-off and risk note

## Example story shape

```md
# STORY: STORY-004

## Goal
Introduce an admin-driven user invite flow across frontend, identity backend, and email delivery.

## Lane
- architectural

## Repositories involved
- repo:web-app
- repo:identity-api
- repo:notification-worker

## Constraints
- invite token generation must stay in identity boundary
- frontend must not encode invitation security logic
- onboarding completion must remain auditable

## Architecture note
- location: invitation lifecycle in identity backend
- owner: identity and access boundary
- boundary: web app triggers flow but does not own token semantics
- trade-off: more backend coordination now to avoid permission logic leaking outward
- risk: broken or insecure invite lifecycle if token state is split across repos
```

## Example task breakdown
- TASK-041: define invite token creation endpoint in identity backend
- TASK-042: add admin invite action in frontend
- TASK-043: connect invite email delivery path
- TASK-044: implement invite acceptance route and validation

## Common mistake
Trying to run this as one big Standard task because the user story sounds coherent.
That usually causes:
- mixed ownership,
- leaky boundaries,
- partial implementation with no trustworthy contract model.

## Escalate further if
Create spikes before coding if major unknowns exist around:
- token lifecycle
- permission model
- email delivery guarantees
- onboarding state transitions

# Example: Standard feature

## Scenario
A team wants to add a new "resend confirmation email" action on the account page.
The backend needs one endpoint, and the frontend needs one button and success/error handling.
The ownership is clear, and the contract is modest.

## Why this is Standard
- meaningful behavior change
- more than a typo or local tweak
- touches multiple implementation units
- still has clear ownership and low architectural uncertainty
- not large enough to require a full cross-repo architectural story

## Required artifacts
- one task or small task set
- light spec only if it clarifies acceptance
- architecture sanity check

## Example architecture sanity

```md
- location: resend logic in `repo:identity-api`, account verification service
- owner: identity backend
- boundary: frontend triggers the action but must not own resend rules
- trade-off: a small extra endpoint now keeps account verification rules centralized
- risk: repeated resend spam if throttling is forgotten
```

## Good task shape

```md
# TASK: TASK-028

## Summary
Add resend confirmation email action to account page.

## Lane
- standard

## Repositories
- repo:web-app
- repo:identity-api

## Goal
Allow a user with an unconfirmed account to request a new confirmation email.

## Acceptance
- [ ] Backend exposes resend endpoint
- [ ] Frontend shows resend action only when relevant
- [ ] User sees success/error feedback
- [ ] Basic abuse protection or throttle path is respected
```

## Common mistake
Treating this as Tiny because the UI change looks small.
That usually hides the fact that:
- backend ownership matters,
- abuse/throttling matters,
- and contract placement matters.

## Escalate only if
Escalate to Architectural if new evidence shows that:
- confirmation state is spread across multiple repos unpredictably
- account verification rules are currently duplicated in the frontend
- the work actually changes auth or identity boundaries broadly

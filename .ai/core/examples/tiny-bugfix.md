# Example: Tiny bugfix

## Scenario
A user reports that the "Save changes" button in the frontend settings page says "Save chagnes".
The typo is isolated to one UI component in one repository.

## Why this is Tiny
- one repo
- one known owner
- no contract or boundary change
- no architectural ambiguity
- low blast radius if wrong

## Required artifacts
- one task only

No spec is needed.
No story is needed.
Architecture sanity is optional because ownership is obvious and no boundary is being changed.

## Good task shape

```md
# TASK: TASK-014

## Summary
Fix typo in settings page save button label.

## Lane
- tiny

## Repositories
- repo:web-app

## Goal
Correct the button label so the UI text is spelled properly.

## Acceptance
- [ ] Settings page button shows "Save changes"
- [ ] No other labels changed
```

## Common mistake
Turning this into process theater:
- writing a full spec
- creating a story
- pretending a typo fix needs architecture review

That creates more system weight than delivery value.

## Escalate only if
Escalate out of Tiny only if the "typo" reveals something bigger, for example:
- the label comes from a broken localization pipeline
- multiple repos or shared content sources are affected
- the fix requires changing a shared UI contract or translation system

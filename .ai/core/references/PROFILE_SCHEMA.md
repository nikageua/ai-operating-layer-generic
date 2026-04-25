# Profile Schema

Concrete profiles live in `project/AGENT_PROFILES/`.
This file defines what a good project-level profile should contain.

## Required fields

- **Profile id**
- **Applies to**: repos, stack, or situations
- **Use for**: tasks this profile handles well
- **Avoid when**: situations that need escalation or another profile
- **Validation**: the smallest meaningful validation steps
- **Escalate when**: clear triggers for stopping or rerouting

## Good profile characteristics

A good profile is:
- specific enough to be useful,
- small enough to stay maintainable,
- grounded in actual repo behavior,
- focused on recurring work, not one-off history.

## Bad profile characteristics

A bad profile:
- duplicates full repo documentation,
- encodes temporary local environment details,
- mixes general doctrine with project-specific quirks,
- keeps growing with every isolated incident.

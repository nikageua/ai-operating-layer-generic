# Cross-Repo Impact Discovery

AIL v2 uses logical repo IDs, but naming repos is not enough.
The system also needs guidance for discovering when a "local" change is actually cross-repo in impact.

## Trigger signals

Raise a cross-repo sanity check when:
- a change touches a contract consumed elsewhere,
- a shared domain concept changes shape,
- auth, identity, billing, permissions, or shared state are involved,
- one repo assumes behavior implemented in another,
- a local fix requires mirrored changes in tests, workers, or UI clients elsewhere.

## Questions to ask
- Is this really local, or am I changing a contract?
- Which other repo consumes this behavior?
- Is there a hidden downstream dependency?
- Does this require lane escalation from Standard to Architectural?

## Rule

When hidden coupling is discovered, lane escalation is healthier than pretending the change stayed local.

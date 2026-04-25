# Promotion Rules

Move something from runtime attempts into durable project docs only when at least one is true:
- it repeated 2 or more times,
- it caused an expensive failure,
- it has broad blast radius,
- it materially improves future decision quality.

## Promote to `KNOWN_PITFALLS.md`
When the lesson is mainly about recurring failure modes.

## Promote to `TECHNICAL_PATTERNS.md`
When the lesson is mainly about a reusable successful approach.

## Promote to `ARCHITECTURAL_CONSTRAINTS.md`
When the lesson defines or protects a boundary.

If the lesson is too local, too temporary, or too narrow, keep it in runtime only.

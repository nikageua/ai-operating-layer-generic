# tasks.json Specification

`tasks.json` is the **acceptance criteria file for a sub-agent profile's harness**.
It defines what a passing harness looks like, in measurable terms.

It lives at the root of the project being optimised by metaharness — not inside `.ai/`.
One `tasks.json` exists per profile/project pair.

---

## Location

```
[project-root]/tasks.json          ← for a project-level harness
[repo-root]/tasks.json             ← for a per-repository harness
```

The path is declared in `metaharness.json` via the `"tasks_file"` field.
The corresponding template is in `.ai/metaharness/tasks.template.json`.

---

## Ownership and Tier

`tasks.json` is a **Tier 3 file** (see `HARNESS_UPDATE_PROTOCOL.md`).

| Operation | Who | Approval |
|-----------|-----|----------|
| Read | Any agent | None needed |
| Add a check | Orchestrator proposes | Human `Yes` required |
| Remove a check | Orchestrator proposes | Human `Yes` required |
| Change a weight | Orchestrator proposes | Human `Yes` required |
| Change expected exit code | Orchestrator proposes | Human `Yes` required |

**No agent may modify `tasks.json` without an explicit `Yes` from the human.**

The metaharness loop reads `tasks.json` to score candidates — it never writes to it.

---

## Schema

Each entry in `tasks.json` is one acceptance check. Two types are supported:

### Type: `file_phrase`

Checks that a specific file contains required phrases.

```json
{
  "id": "unique-check-id",
  "description": "Human-readable explanation of what this checks",
  "type": "file_phrase",
  "path": "relative/path/to/file.md",
  "weight": 1.0,
  "required_phrases": [
    "exact phrase that must appear in the file",
    "another required phrase"
  ]
}
```

- `weight`: contribution to the total score if this check passes. Use `0.5` for low-importance checks, `1.0` for standard, `2.0` for critical.
- All phrases must be present for the check to pass (AND logic).

### Type: `command`

Runs a shell command and checks its exit code.

```json
{
  "id": "unique-check-id",
  "description": "Human-readable explanation of what this checks",
  "type": "command",
  "weight": 1.0,
  "command": "bash scripts/test.sh",
  "expect_exit_code": 0
}
```

- Commands run from the project baseline directory.
- Prefer commands that are fast and idempotent.
- Test commands should be the highest-weight checks.

---

## Scoring

The metaharness loop scores each candidate as:

```
score = sum(weight of each passing check) / sum(weight of all checks)
```

Expressed as a percentage. Thresholds (from `HARNESS_UPDATE_PROTOCOL.md`):
- `draft → validated`: score ≥ 70%
- `validated → stable`: score = 100% on 3 consecutive runs

---

## When to Add a Check

Add a check to `tasks.json` when:

1. **Harness bootstrap completes** — the bootstrap agent proposes initial checks for the new profile
2. **A recurring failure is discovered** — e.g. agents keep missing a required instruction → add a `file_phrase` check
3. **A new script is added to the harness** — add a `command` check for it
4. **A spec acceptance criterion maps to a harness property** — codify it as a check

Propose additions using the standard AI layer update format:

```
Proposed AI layer update:

Harness
- tasks.json: add check — id: [check-id], type: [type], weight: [weight]
  reason: [why this check is needed]
  evidence: [task or failure that triggered this]

Approve AI layer update? (Yes / No)
```

---

## When to Remove or Reweight a Check

Remove a check when:
- The file or script it checks no longer exists
- The check is consistently passing and provides no signal (consider keeping for safety)
- The check is consistently failing because the harness deliberately moved away from that pattern

Reweight a check when:
- Experience shows it is more or less critical than its current weight suggests

Removal and reweighting follow the same Tier 3 proposal process as additions.

---

## Relationship to Profile Files

Each profile in `.ai/agents/profiles/[id].md` declares:
- `## Bootstrap Command` — should have a corresponding `command` check
- `## Validate Command` — should have a corresponding `command` check
- `## Test Command` — should have a corresponding `command` check with `weight: 2.0`
- `## Key Instructions For Sub-Agent` — key phrases here should appear as `file_phrase` checks in `AGENTS.md`

When a profile is updated (Tier 2), verify that `tasks.json` still reflects the profile's
expected harness state. Propose `tasks.json` updates alongside profile updates if needed.

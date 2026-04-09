# Profile: generic

## Status
stable

## Target Environment
- Repository: any
- Language: any
- Framework: any
- Package manager: any

## Purpose
Fallback profile used when no framework-specific profile exists yet,
or for tasks that are framework-agnostic (documentation, config, CI, AI layer updates).

## Required Tools / Skills
- Read / Write / Edit: file manipulation
- Bash: running shell commands
- No framework-specific skills required

## Bootstrap Command
```bash
# No standard bootstrap for generic profile.
# Sub-agent must inspect the repository and determine setup steps.
echo "No bootstrap defined for generic profile. Inspect repository first."
```

## Validate Command
```bash
# Check that key AI layer files exist
test -f .ai/agent/AGENTS.md && echo "AGENTS.md present" || echo "AGENTS.md missing"
```

## Test Command
```bash
# No standard test for generic profile.
# Sub-agent must determine test command from repository context.
echo "No test defined for generic profile. Inspect repository first."
```

## Key Instructions For Sub-Agent
- Read `.ai/agent/AGENTS.md` and all brain files before starting.
- Do not invent framework conventions — inspect the repository first.
- Prefer small, targeted changes over large rewrites.
- Do not modify files outside the active task's stated scope.
- After completing the task, propose an AI layer update for approval.

## Known Pitfalls
- Generic profile has no environment validation. If the task fails unexpectedly,
  trigger harness bootstrap to create a framework-specific profile.

## Metaharness Optimization History
- initial — generic fallback created

# Harness Bootstrap Protocol

When a task requires a sub-agent profile that does not yet exist,
the agent must run the bootstrap protocol before the task can start.

This solves the "empty start" problem: you cannot define harness rules
for a repository you haven't inspected yet.

---

## When Bootstrap Is Triggered

Bootstrap is needed when:
1. A task declares `## Agent Profile: [profile-id]` and that profile file does not exist
2. A new repository is added to the feature scope in a spec
3. An existing profile is marked `deprecated` and a replacement is needed

---

## Bootstrap Steps

### Step 1: Inspect the target repository

The agent must read the target repository and collect:

```
- primary language and version (e.g. TypeScript 5.x, C# 12)
- framework and version (e.g. Angular 17, .NET 8, NestJS 10)
- package manager (npm, pnpm, yarn, dotnet, etc.)
- test runner and command (e.g. jest, xunit, nunit)
- lint / format tooling (e.g. eslint, prettier, dotnet format)
- build command
- existing AGENTS.md or GEMINI.md content (if any)
- existing scripts/ folder (if any)
- CI config (if any, to learn what passing looks like)
```

### Step 2: Generate a draft profile

Create a new file in `.ai/agents/profiles/[profile-id].md` using the
PROFILE_TEMPLATE structure (see below).

Fill every section from what was discovered in Step 1.
Mark the profile status as `bootstrap`.

### Step 3: Generate initial tasks.json entries

For the new profile, propose additions to `tasks.json` that cover:
- a `file_phrase` check for the key instruction in AGENTS.md
- a `command` check for the bootstrap script
- a `command` check for the test script

Propose these as an AI layer update and wait for approval before writing.

### Step 4: Create a harness validation task

Before the real task starts, create a `[harness]` task in `.ai/tasks/ready/`:

```
TASK_ID — [harness] Validate bootstrap profile for [profile-id]

## Epic
[parent epic or standalone]

## Agent Profile
generic

## Goal
Run the initial harness baseline for [profile-id] and confirm bootstrap, validate, and test scripts exit 0.

## Acceptance Criteria
1. scripts/bootstrap.sh exits 0
2. scripts/validate.sh exits 0
3. scripts/test.sh exits 0
4. Profile status updated from bootstrap → draft
```

Only after this validation task is done may the real task proceed.

---

## Profile Template

```markdown
# Profile: [profile-id]

## Status
bootstrap | draft | validated | stable | deprecated

## Target Environment
- Repository: [repo name or path]
- Language: [language + version]
- Framework: [framework + version]
- Package manager: [tool]

## Required Tools / Skills
- [tool or skill name]: [why it is needed]
- [tool or skill name]: [why it is needed]

## Bootstrap Command
[command to set up the environment from scratch]

## Validate Command
[command that checks the harness files are structurally correct]

## Test Command
[command that runs the full test suite]

## Build Command
[command that produces a build artifact]

## Key Instructions For Sub-Agent
[3–5 bullet points the sub-agent must follow in this environment]
- ...
- ...

## Known Pitfalls
[Things that have gone wrong before or are likely to go wrong]
- ...
- ...

## Metaharness Optimization History
[Filled in automatically by the metaharness loop after each run]
- [date] — [what changed] — [score before → after]
```

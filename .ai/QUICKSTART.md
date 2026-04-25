# Quickstart

## 1. Copy the template once

Copy `.ai/` and `INIT_PROMPT.md` into your shared workspace or project root.

Do not create one full AIL copy per user story.

## 2. Fill the project overlay

Start with:
- `.ai/project/PROJECT_CONTEXT.md`
- `.ai/project/REPO_REGISTRY.yaml`
- `.ai/project/CONVENTIONS.md`
- `.ai/project/ARCHITECTURAL_CONSTRAINTS.md` if needed
- `.ai/project/AGENT_PROFILES/`

## 3. Set local machine mapping

Create locally:
- `.ai/runtime/local-map.yaml`

Do not commit machine-specific paths or local URLs.

## 4. Pick a lane for each change

- Tiny
- Standard
- Architectural

## 5. Use story folders for multi-repo work

For non-trivial or cross-repo work, create:
- `.ai/project/stories/STORY-xxx/`

Use logical IDs only in tracked story docs.

## 6. Learn through failures, not bureaucracy

When a task gets blocked:
- classify the failure
- choose a new valid next move
- record attempts locally only when useful
- promote repeated lessons into project docs


See also: `.ai/core/references/NAMING_AND_IDS.md` for collision-resistant artifact naming.

## Grow only as needed

Do not fill every layer on day one. Start minimal, then adopt stronger doctrine as parallel work and repeated lessons make it necessary.

## Keep startup lean

For a fresh session, load only the minimal bootstrap doctrine first. Pull in additional doctrine only when the problem actually requires it.

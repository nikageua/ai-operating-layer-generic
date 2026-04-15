# AI Quickstart

 > **Read this file first, every session** — shared rules, commands, and pitfalls.
 > Then read your personal `.ai/QUICKSTART.local.md` for your active task and recent decisions.
 > If `QUICKSTART.local.md` doesn't exist yet, create it from the template at the bottom of this file.

 ---

 ## Hard Rules

 - **Never create epics without an approved spec.**
 - **Never write code without an active task.**
 - **Never modify `.ai/` files without proposing an update and receiving explicit "Yes" approval.**
 - One task in-progress at a time (unless explicitly parallelized by the orchestrator).
 - Sub-agents propose `.ai/` changes — they do not apply them directly.

 ---

 ## Key Commands

 > ⚠️ Fill in project-specific commands when adopting this template.

 ```bash
 # Example — replace with your actual build/test commands:
 # npm run build
 # dotnet build
 # npm test

-------------------------------------------------------------------------------------------------------------------------

Top Pitfalls

 ⚠️ Fill in project-specific pitfalls when adopting this template. Add entries here as you discover recurring failure
 modes.

-------------------------------------------------------------------------------------------------------------------------

QUICKSTART.local.md Template

QUICKSTART.local.md is gitignored — each developer maintains their own copy. Create .ai/QUICKSTART.local.md and fill it
in:

 # My Quickstart

 ## Active Task
 **[TASK-ID]** — [Task title]
 Epic: [EPIC-ID]

 Next steps:
 1. ...

 ## Recent Decisions
 - [YYYY-MM-DD] ...

 ## Open Notes
 - ...

-------------------------------------------------------------------------------------------------------------------------

 For full read/update rules for every AI layer file, see .ai/agent/AGENTS.md.
# AI Operating Layer

Reusable AI operating system for a repository.

Purpose:
- give AI agents stable project context
- enforce scoped incremental work
- reduce manual coordination
- keep repository state synchronized with AI-visible state

Layers:
- `agent/` — rules for agent behavior
- `architecture/` — technical constraints and implementation boundaries
- `project/` — stable project context
- `brain/` — current working state
- `tasks/` — operational task pipeline
- `memory/` — durable patterns and lessons

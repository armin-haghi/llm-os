---
name: orchestrator
description: Use the single cross-interface orchestration path for project sweeps and selected-project agent work.
---

# Orchestrator

Use this skill when the human wants to refresh projects or start work from the
shared orchestration path, regardless of whether the interface is OpenClaw,
Codex, Claude, ChatGPT, or another assistant.

## Commands

### Project sweep

Trigger phrases:
- "go through my projects"
- "make sure my projects are up to date"
- "refresh the control tower"

Use:
- `orchestration/prompts/project-sweep.md`

Output:
- refreshed Project Control Tower
- refreshed Agent Run Queue
- concise human summary of active, stale, blocked, waiting-human, and ready
  work

### Start project work

Trigger phrases:
- "start orchestrating work on <project>"
- "continue <project>"
- "pick up <project>"

Use:
- `orchestration/prompts/start-project-work.md`

Output:
- one selected or created bounded run
- run status update
- project write-back if state changes
- human decision request only when needed

## Rules

- This is the one path across assistant entrypoints.
- Notion is the portfolio and run-dispatch surface.
- Repo docs remain the execution source of truth after repo creation.
- Avoid making the human reconstruct thread context.
- Do not create backlog-style run records.
- Do not create GitHub issues by default; issues are optional only when the
  project already uses them as its execution surface or the human explicitly
  asks for issue-based tracking.
- A run is ready only when an agent can start from declared inputs.

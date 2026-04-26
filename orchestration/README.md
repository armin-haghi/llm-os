# Orchestration Path

This is the single human-facing path for multi-project agent work.

It can be used from OpenClaw, Codex, Claude, ChatGPT, or any future assistant
entrypoint. The interface may differ, but the workflow should not.

The human should be able to ask:

1. "Go through my projects and make sure they are all up to date."
2. "Start orchestrating work on this project."

Notion may be used as the portfolio and run-dispatch surface, but repo docs
remain the execution source of truth once a repo exists.

## Surfaces

- Project Control Tower:
  private Notion database named `Project Control Tower`
- Agent Run Queue:
  private Notion database named `Agent Run Queue`
- Project overview input:
  `templates/project-overview.yaml`
- Agent run input:
  `templates/agent-run.yaml`

If an assistant has Notion access, it should resolve the Notion surfaces by
name. If it does not, use `.llm-os.local.yaml` locally or ask the human for
access to the private Notion workspace.

## Workflow 1: Project Sweep

Use `orchestration/prompts/project-sweep.md`.

Purpose:
- refresh all known project records
- identify stale projects
- update the Project Control Tower
- create or update bounded Agent Run Queue records
- surface only real human decisions

Output:
- updated Notion project records
- updated run queue records
- a short human summary of active, stale, blocked, waiting-human, and ready
  agent work

## Workflow 2: Start Project Work

Use `orchestration/prompts/start-project-work.md`.

Purpose:
- take one project chosen by the human
- pick or create one bounded run
- dispatch work using the declared read path and write-back targets
- interact with the human only when judgment, access, priority, or risk
  acceptance is needed

Output:
- run status updated in Notion
- project docs updated if project state changes
- result handoff written back before the run closes

## Rules

- This is the interaction path, not the source of truth.
- Do not make the human manage individual agent threads manually.
- Do not create vague run records.
- A ready run must include input source, read path, write-back targets, and a
  bounded goal.
- A blocked or waiting-human run must say exactly what is needed from the human.
- A done run must include a result handoff and durable write-back status.

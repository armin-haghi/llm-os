# Orchestration Path

This is the single human-facing path for multi-project agent work.

It can be used from OpenClaw, Codex, Claude, ChatGPT, or any future assistant
entrypoint. The interface may differ, but the workflow should not.

For first-time setup, read `SETUP.md` before using this path.

The human should be able to ask:

1. "Go through my projects and make sure they are all up to date."
2. "Start orchestrating work on this project."
3. "Audit this project for LLM-OS gaps."

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
- LLM-OS version standard:
  `llm-os-docs/version-log.md`

If an assistant has Notion access, it should resolve the Notion surfaces by
name. If it does not, use `.llm-os.local.yaml` locally or ask the human for
access to the private Notion workspace.

## Workflow 1: Project Sweep

Use `orchestration/prompts/project-sweep.md`.

Purpose:
- refresh all known project records
- identify stale projects
- classify repo/Notion source-of-truth alignment
- check each project's `llm_os_version` against the current standard
- update the Project Control Tower
- create or update bounded Agent Run Queue records
- surface only real human decisions

Output:
- updated Notion project records
- updated run queue records
- source-of-truth alignment summary
- LLM-OS compatibility update summary
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

## Workflow 3: Project Audit

Use `orchestration/prompts/project-audit.md`.

Purpose:
- check whether one project is ready for `llm-os` orchestration
- identify missing entrypoints, project state, milestone clarity, run readiness,
  human-decision capture, source-of-truth boundaries, compatibility state, and
  resume quality
- classify the project as `ready`, `blocked`, `needs-sync`,
  `needs-migration`, `not-ready`, or `unknown`

Output:
- one overall readiness classification
- audit table with status, finding, and fix
- compact YAML-style summary
- recommended next action
- whether to create or update an Agent Run Queue item

## Consistency rule

Before reporting a project as current, classify it as one of:

- `aligned`
- `repo-newer-than-notion`
- `notion-newer-than-repo`
- `unknown`

Repo docs decide execution state once a repo exists.
Notion decides portfolio state, run dispatch, blockers, and human decisions.
Completed run records are historical unless they explicitly say they are the
latest state as of a commit.

## Compatibility rule

The current LLM-OS standard is declared in `llm-os-docs/version-log.md`.
Project sweeps and audits should compare each repo's `project-overview.yaml`
against that standard using:

- `llm_os_version`
- `llm_os_profile`
- `llm_os_last_checked`
- `llm_os_update_needed`
- `llm_os_update_reason`

If a repo is behind the current standard, create or update one bounded migration
run instead of scattering many small tasks.

## Rules

- This is the interaction path, not the source of truth.
- Do not make the human manage individual agent threads manually.
- Do not create vague run records.
- A ready run must include input source, read path, write-back targets, and a
  bounded goal.
- A blocked or waiting-human run must say exactly what is needed from the human.
- A done run must include a result handoff and durable write-back status.
- Do not treat version drift as an emergency unless it blocks the selected work.
- Do not turn project audits into broad product critiques.

# Minimal Control Tower

Status: active

This note defines the first control-tower and agent-run orchestration slice for
`llm-os`.

The control tower is a cross-project visibility layer.
The agent run queue is a bounded session-orchestration layer.

Neither is a replacement for repo-local project docs.

## Purpose

Use the control tower to answer:
- what projects are active right now
- which projects are stale
- which projects are blocked
- which projects need a human decision
- which projects show commercialization signal

It exists to make portfolio state visible without moving execution out of the
repo once a repo exists.

Use the agent run queue to answer:
- what an agent can pick up next
- what context the agent must load
- what the agent is allowed to change
- where the agent must write back
- what is blocked on human input
- which thread or run owns the current work

It exists to reduce manual thread management without turning Notion into a
competing project execution surface.

The shared orchestration path is the preferred human-facing front door for this
layer.
The human should be able to ask any supported assistant entrypoint to refresh
project state or start work on a chosen project without personally managing
separate agent threads.

## Boundary

The first control-tower slice must keep these roles explicit:

- repo docs
  - active execution source of truth once a repo exists
- `project-overview.yaml`
  - minimum structured project input for cross-project rollups
- Notion
  - portfolio view, project summary, agent run queue, comments, ownership,
    blockers, priorities, and human decisions
- orchestration path
  - human-facing workflow that reads Notion and repo docs, creates or selects
    bounded runs, and interacts with the human only where judgment or access is
    required

Rule:
- before a repo exists, one canonical Notion page may be the working surface
- after a repo exists and active build starts, the repo becomes the execution
  source of truth
- after that transition, the control tower should summarize project state, not
  carry competing milestone or implementation detail
- agent runs may point to repo-local execution docs and write-back targets, but
  should not duplicate the full implementation plan in Notion
- any assistant using the orchestration path may dispatch work from Notion run
  records, but must write back to the run record and the repo-local project docs
  when project state changes

## Unit of tracking

Track one control-tower record per project.

Do not create:
- one record per session
- one record per milestone
- one record per idea iteration

Use the same project record over time and keep its current state fresh.

Track one agent-run record per bounded agent session or handoff.

Do not create:
- one record per tiny task
- one record per chat message
- one record per vague area of interest

Create a run only when an agent can either execute it from declared inputs or
surface a specific blocker/human decision.

## Minimum fields

The first control-tower slice should carry only the fields needed for
cross-project visibility:

- `project`
  - canonical project name
- `status`
  - `idea`
  - `shaping`
  - `build-ready`
  - `active-build`
  - `parked`
  - `archived`
- `stage`
  - one canonical `llm-os` stage
- `active_milestone`
  - exact current milestone
- `freshness`
  - `current`
  - `stale`
  - `unknown`
- `last_reviewed`
  - `YYYY-MM-DD`
- `owner`
  - human owner or responsible maintainer
- `blocker`
  - current blocker or `none`
- `next_decision`
  - current human decision or `none`
- `next_action`
  - next concrete move
- `canonical_repo`
  - repo link or path, blank before repo creation
- `notion_page`
  - private Notion page link for pre-repo projects or summary/review pages
- `execution_surface`
  - `Notion` before a repo exists
  - `repo` once active build begins
- `commercial_signal`
  - `none`
  - `weak`
  - `moderate`
  - `strong`

`notion_page` is a Notion-side/private field.
Do not require public repo files to contain raw private Notion URLs.

These fields are intentionally minimal.
If a field does not improve portfolio visibility or prioritization, it probably
does not belong in the first slice.

## Minimum views

The first control tower should support these views:

1. `Active projects`
   - projects with `status` in `build-ready` or `active-build`
   - grouped or filtered by `stage`
2. `Needs attention`
   - stale projects
   - blocked projects
   - projects with a non-`none` `next_decision`
3. `Commercial candidates`
   - projects with `commercial_signal` of `moderate` or `strong`
4. `Parked / archived`
   - non-active work kept out of the default active view

## Agent run queue

The first run-queue slice should carry only the fields needed to let an agent
continue work without the human manually reconstructing thread context:

- `run`
  - short action-oriented run name
- `project`
  - project name matching the control-tower project record
- `status`
  - `ready`
  - `in-flight`
  - `waiting-human`
  - `blocked`
  - `done`
  - `stale`
- `priority`
  - `now`
  - `next`
  - `later`
- `agent_contract`
  - the narrow contract or workflow to apply
- `goal`
  - the bounded outcome for the run
- `input_source`
  - repo path, Notion page, issue, PR, or handoff source
- `required_read_path`
  - minimum context the agent must load before acting
- `write_back_targets`
  - durable repo or Notion targets that must be updated before closing
- `human_decision_needed`
  - current decision or `none`
- `result_handoff`
  - completion summary, blocker, or next-run handoff
- `thread_link`
  - chat, PR, issue, or run link when available
- `canonical_repo`
  - repo link or path
- `last_touched`
  - `YYYY-MM-DD`

Minimum run-queue views:

1. `Ready for agents`
   - `status` is `ready`
2. `In flight`
   - `status` is `in-flight`
3. `Waiting human`
   - `status` is `waiting-human`
4. `Blocked`
   - `status` is `blocked`
5. `Done`
   - recent completed runs with result handoffs

Rules:
- a ready run must include enough input and read-path context for an agent to
  start without asking the human to reconstruct the thread
- an in-flight run should name the current thread or handoff when possible
- a blocked or waiting-human run must say exactly what is needed
- a done run must include a result handoff and any write-back that changed
  project state
- if a run changes active milestone, blocker, next action, or human decision,
  update the project-level repo docs and the project control-tower record

## Freshness rule

The control tower should help expose stale work, not hide it.

Practical default:
- active projects should have a recent `last_reviewed`
- if the project has not been reviewed recently, set `freshness` to `stale`
- if the next action or next decision is no longer real, the record is not
  current

The control tower should not silently treat neglected projects as active.

## Update rules

Update the control-tower record when:
- the active milestone changes materially
- the project moves stage
- the project becomes blocked or unblocked
- the next human decision changes
- freshness changes
- the execution surface changes from `Notion` to `repo`

Do not update the control tower for minor implementation churn that does not
change portfolio state.

Update the agent run queue when:
- a run is created, started, blocked, handed off, or completed
- the owning thread changes
- the required human decision changes
- the write-back target changes
- the result handoff changes

Do not use the run queue as a task backlog.
It is for bounded agent sessions and handoffs, not every implementation step.

## Input sources

Use the same logical shape across tools:

- before repo creation
  - one canonical Notion page with the minimum fields, linked from the control
    tower's `Notion Page` field
- after repo creation
  - `project-overview.yaml` in the repo
- during portfolio refresh
  - one or more project-overview inputs plus any current portfolio summary

The storage location may differ.
The control-tower shape should not.

## First-slice non-goals

Do not add:
- backlog-style task tracking
- milestone histories
- detailed meeting notes
- per-session logs
- automation-heavy workflow logic
- a second review system

If a field or view feels like project management overhead, leave it out of the
first slice.

## Practical default

The first useful implementation is:
- one record per active project
- one record per active agent run
- one minimal schema
- a small set of views
- clear repo/Notion boundaries

That is enough to reduce stale docs, improve prioritization, and reduce manual
thread management without turning the control tower into a new operating
system.

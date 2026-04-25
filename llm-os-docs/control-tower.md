# Minimal Control Tower

Status: active

This note defines the first control-tower slice for `llm-os`.

The control tower is a cross-project visibility layer.
It is not a second execution surface, not a backlog system, and not a
replacement for repo-local project docs.

## Purpose

Use the control tower to answer:
- what projects are active right now
- which projects are stale
- which projects are blocked
- which projects need a human decision
- which projects show commercialization signal

It exists to make portfolio state visible without moving execution out of the
repo once a repo exists.

## Boundary

The first control-tower slice must keep these roles explicit:

- repo docs
  - active execution source of truth once a repo exists
- `project-overview.yaml`
  - minimum structured project input for cross-project rollups
- Notion
  - portfolio view, project summary, comments, ownership, blockers, priorities,
    and human decisions

Rule:
- before a repo exists, one canonical Notion page may be the working surface
- after a repo exists and active build starts, the repo becomes the execution
  source of truth
- after that transition, the control tower should summarize project state, not
  carry competing milestone or implementation detail

## Unit of tracking

Track one control-tower record per project.

Do not create:
- one record per session
- one record per milestone
- one record per idea iteration

Use the same project record over time and keep its current state fresh.

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
- `execution_surface`
  - `Notion` before a repo exists
  - `repo` once active build begins
- `commercial_signal`
  - `none`
  - `weak`
  - `moderate`
  - `strong`

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

## Input sources

Use the same logical shape across tools:

- before repo creation
  - one canonical Notion page with the minimum fields
- after repo creation
  - `project-overview.yaml` in the repo
- during portfolio refresh
  - one or more project-overview inputs plus any current portfolio summary

The storage location may differ.
The control-tower shape should not.

## First-slice non-goals

Do not add:
- task tracking
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
- one minimal schema
- a small set of views
- clear repo/Notion boundaries

That is enough to reduce stale docs and improve prioritization without turning
the control tower into a new operating system.

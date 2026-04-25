---
name: agent-run
description: Pick up and advance one bounded run from the Agent Run Queue.
---

# Agent Run

Use this skill when a run has been selected from the Agent Run Queue or when
the user asks an agent to continue queued project work.

## Read

1. the selected run record, shaped like `templates/agent-run.yaml` or the
   equivalent Notion Agent Run Queue row
2. the run's declared input source
3. the run's required read path
4. project-level canonical docs only as needed for the selected run

## Execute

- confirm the run has a bounded goal
- load only the declared context needed to start
- apply the named agent contract or workflow
- do the work if it can proceed safely
- surface the exact blocker or human decision if it cannot proceed

## Write back

Update the run record with:
- status
- result handoff
- thread link when available
- last touched date

Update project-level write-back targets when the run changes:
- active milestone
- blocker
- next action
- human decision
- freshness
- stage or status

## Rules

- do not treat the run queue as the project execution source of truth
- do not rewrite project milestone intent without project-level evidence
- do not expand a run into a broad backlog
- if the run is underspecified, mark it `waiting-human` or `blocked` with the
  specific missing decision/input
- before closing a completed run, make the durable write-back explicit

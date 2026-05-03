---
name: morning-status-brief
description: Produce a read-only morning project status from the LLM-OS Project Control Tower and Agent Run Queue.
---

# Morning Status Brief

Use this skill when the human asks for:

- "morning project status"
- "morning status"
- "project status"
- "queue status"
- "what needs my decision today"
- "what should I work on today"

This skill produces a daily operating brief from the canonical `llm-os` portfolio
and run surfaces:

- Project Control Tower
- Agent Run Queue

Default behavior is read-only. Do not update Notion, repo docs, or run records
unless the human explicitly asks.

## Private surface rule

Do not commit or rely on private Notion IDs, page URLs, database IDs,
data-source IDs, or connector-specific IDs in this skill.

Resolve private surfaces by:

1. connected workspace/tool search using the canonical names `Project Control
   Tower` and `Agent Run Queue`
2. a link supplied by the human in the current session
3. ignored local config such as `.llm-os.local.yaml` for private local workflows
4. asking the human for access or pasted content if needed

## Data access order

Prefer direct data-source/database query when the current connector supports it.

If direct query is unavailable, fall back to:

1. search the Project Control Tower and Agent Run Queue by canonical name or
   data-source scope
2. fetch individual result pages
3. extract fields from page properties

Do not ask the human to summarize project status if the Notion surfaces are
accessible.

If a tool cannot access one surface, report partial results and name the missing
surface.

## Read from Project Control Tower

Read these fields when available:

- Project
- Status
- Stage
- Active Milestone
- Freshness
- Last Reviewed
- Owner
- Blocker
- Next Decision
- Next Action
- Canonical Repo
- Execution Surface
- Commercial Signal
- Notion Page
- Repo Branch
- Repo Latest Commit
- Repo State Checked
- Repo Review Needed
- Repo Review Reason
- Repo Review Agent

Classify projects:

- `active`: status is `active-build`
- `ready`: status is `build-ready`
- `shaping`: status is `shaping`
- `parked`: status is `parked`
- `archived`: status is `archived`
- `stale`: freshness is `stale` or `unknown`

## Read from Agent Run Queue

Read these fields when available:

- Run
- Project
- Status
- Priority
- Agent Contract
- Goal
- Human Decision Needed
- Result Handoff
- Input Source
- Required Read Path
- Write Back Targets
- Last Touched

Classify runs:

- `waiting_human`: status is `waiting-human`
- `blocked`: status is `blocked`
- `in_flight`: status is `in-flight`
- `ready`: status is `ready`
- `historical`: status is `done` or `stale`

## Morning brief structure

Return markdown by default.

Use this order:

1. Portfolio picture
2. Active / ready / shaping projects
3. Waiting-human decisions
4. Blocked work
5. In-flight runs
6. Ready agent runs
7. Repo review / refresh needed
8. Parked projects
9. Recommended starts today

Only use an interactive widget if the current client explicitly supports one.
The markdown brief must stand on its own.

## Portfolio picture

Show compact counts:

- active-build projects
- build-ready projects
- shaping projects
- parked projects
- waiting-human runs
- blocked runs
- in-flight runs
- ready runs
- stale/unknown projects
- repo review-needed projects

## Waiting-human decisions

This is the most important section.

Order by:

1. priority `now`
2. blocked projects
3. active-build projects
4. build-ready projects
5. shaping projects
6. parked projects only if they have an explicit revisit trigger

For each decision, show:

- project
- decision needed
- why it matters
- default if not answered, if obvious
- run name, if tied to a run

## Repo review / refresh needed

Surface projects where:

- `Repo Review Needed` is `yes` or `unknown`
- `Repo Latest Commit` is behind the actual repo head, when repo access exists
- the repo head changed after the last known Project Control Tower or run
  handoff
- a build/coding/debug/ship run changed repo files and no separate review or
  refresh has cleared it

Use:

- `review-gate` when correctness, quality, tests, safety, or acceptance should
  be checked
- `project-refresh` when repo docs, Notion, and run state need synchronization

Do not clear review-needed state during the morning brief.

## Recommended starts today

Recommend at most three actions.

Default preference:

1. Clear one decision that unlocks an active project.
2. Start one ready agent run.
3. Run one review/refresh agent if repo state changed.
4. Review one stale or needs-sync project only if it blocks active work.

Do not recommend parked projects unless the human explicitly asks or the project
has a concrete revisit trigger.

## Source-of-truth rules

- Repo docs decide execution state once a repo exists.
- Notion decides portfolio state, run dispatch, blockers, and human decisions.
- Completed and stale Agent Run Queue records are historical.
- GitHub issues are not default tracking surfaces.
- Do not create new tasks during the morning brief unless the human asks.

## Output format

Use concise tables.

End with:

```text
Recommended next command:
<one suggested command>
```

## Write-back

Morning status is read-only by default.

Only write back when the human explicitly asks, for example:

- mark a run done
- mark a project parked
- update a decision
- update next action
- create a new Agent Run Queue item
- update repo review-needed state after a separate review/refresh action

## Failure handling

If direct query fails:

1. retry once with search plus fetch
2. report partial results
3. explicitly say which surface could not be read

Never invent project state.

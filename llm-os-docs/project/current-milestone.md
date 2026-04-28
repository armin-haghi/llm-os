# Current Milestone

## Snapshot
- Project: `llm-os`
- Stage: `Prototype`
- Milestone: test and harden the minimal control-tower, Agent Run Queue, and shared orchestration path across active projects
- Owner: human maintainer with agent support
- Status: `active`
- Last updated: `2026-04-28`

## Why this milestone matters

The first control-tower and Agent Run Queue slice exists in both repo docs and
Notion. The next highest-value gap is no longer defining the first shape. It is
proving that the shape can drive real parallel product work without creating a
second project-management system or second execution truth.

If it succeeds:
- active projects can be refreshed from one shared orchestration path
- stale or contradictory Notion state can be detected and repaired
- agents can pick up bounded runs without the human manually reconstructing
  thread context
- repo docs remain canonical for execution once a project has a repo
- Notion remains the portfolio, run-dispatch, blocker, and human-decision layer
- the system can support parallel product streams with clear write-back rules

Further expansion should wait until this path is tested against real active
projects, because adding more schema or skills before validation would likely
increase coordination noise.

## In scope

- run a project sweep using the shared orchestration path
- test selected-project work through the Agent Run Queue
- verify that a bounded run can start from declared input, read path, and
  write-back targets
- reconcile Notion state from repo docs when repo docs are fresher
- update project-level repo docs when project state changes
- identify the smallest durable consistency check that prevents Notion/repo
  drift without adding bureaucracy
- decide whether parallel work streams need a first-class object or can remain
  represented as project milestones plus bounded agent runs for now

## Out of scope

- full task/backlog management
- detailed milestone history tracking
- heavy automation or concurrency implementation
- stage-skill expansion before orchestration validation
- broad historical rewrites of every background note
- treating Notion as the execution source of truth after repo creation

## Acceptance criteria

- the Project Control Tower and Agent Run Queue can be used on `llm-os`,
  Costmind, and one more active project without manual thread reconstruction
- `AGENTS.md` routes agents to the orchestration path for project sweeps and
  selected-project work
- stale completed run handoffs do not masquerade as latest repo state
- Notion views do not hide relevant active, commercial, waiting-human, blocked,
  or done work
- repo-local docs remain canonical after repo creation
- a project sweep can identify and repair source-of-truth drift
- the next roadmap decision is grounded in observed orchestration use, not only
  conceptual design

## Dependencies

- active project examples to test against
- Notion access for Project Control Tower and Agent Run Queue updates
- repo access for `project-overview.yaml` and live project-doc updates
- willingness to keep the orchestration slice minimal until it proves useful

## Blockers

- none currently
- residual risk remains around stale Notion records and hidden view filters if
  project sweeps are not run consistently

## Open questions to clarify during active sessions

- what is the smallest durable consistency check that prevents Notion/repo drift
  without adding bureaucracy?
- should parallel work streams become a first-class object, or should they
  remain represented as project milestones plus bounded agent runs for now?

# Current Milestone

## Snapshot
- Project: `llm-os`
- Stage: `Prototype`
- Milestone: define the first minimal control-tower and agent-run layer across projects
- Owner: human maintainer with agent support
- Status: `active`
- Last updated: `2026-04-25`

## Why this milestone matters
The first-cut operating surface has now been accepted as complete enough to
advance. The next highest-value gap is not more repo-local cleanup. It is a
minimal cross-project control layer that makes active work and agent handoffs
visible without turning Notion or portfolio docs into a second execution truth.

If it succeeds:
- active projects can be seen and compared in one place
- stale idea and project pages become easier to identify and retire
- cross-project prioritization and human decisions become visible without
  bloating repo-local execution surfaces
- agents can pick up bounded runs without the human manually reconstructing
  thread context
- one shared orchestration path can act as the human-facing front door for
  project sweeps and selected-project orchestration

Later control-tower expansion should wait for this because a larger portfolio
layer without a minimal working shape would create more coordination noise than
clarity.

## In scope
- define the smallest viable control-tower model for cross-project visibility
- define the smallest viable Agent Run Queue model for bounded agent sessions
- set the boundary between repo docs, `project-overview.yaml`, and Notion
- set the boundary between repo docs, Notion run records, and agent thread
  handoffs
- define the minimum fields and views needed to track project state cleanly
- define the minimum fields and views needed to dispatch and close agent runs
- define the shared prompts/workflow for project sweeps and selected-project
  orchestration
- include freshness and stale-state handling so old idea pages do not linger as
  fake current work
- test the control-tower slice against current active projects
- record the minimum viable checking method that would improve future
  validation confidence without turning review into bureaucracy

## Out of scope
- concurrency rules implementation
- stage-skill expansion
- machine-readable schemas beyond what the first control-tower slice actually
  needs
- broader tool compatibility outputs beyond the current minimal Claude shim
- broad historical rewrites of every background note

## Acceptance criteria
- the control tower has a clear minimum scope and does not become a second PM
  system
- the Agent Run Queue has a clear minimum scope and does not become a backlog
- project-level execution truth remains in repo docs once a repo exists
- the cross-project layer has a clear canonical input shape and update path
- agent runs carry enough input, read-path, and write-back context for agents
  to continue work without human thread management
- the shared orchestration path has a small workflow for refreshing all projects
  and orchestrating a selected project
- freshness and stale handling are explicit enough to reduce zombie Notion docs
- at least one usable project-overview/control-tower path exists for active
  projects
- at least one usable agent-run queue path exists for active project handoffs
- a lightweight validation/checking method is defined as a follow-on
  improvement, even if it is not fully automated yet

## Dependencies
- human decisions about minimum useful project fields and views
- active project examples to test against
- willingness to keep the first slice minimal instead of designing a full
  portfolio system

## Blockers
- none currently
- residual risk remains around stale project metadata if the control-tower layer
  expands before freshness rules are used consistently

## Open questions to clarify during active sessions
- is the first control-tower plus Agent Run Queue schema enough once tested
  against current active projects?
- what is the minimum durable checking method for future validation passes once
  control-tower work starts touching more active projects?

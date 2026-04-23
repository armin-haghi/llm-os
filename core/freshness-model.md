# Freshness Model

This file defines when project context is fresh enough to execute from safely
and when a refresh should happen first.

## Purpose

Use freshness rules to prevent work from running on stale, contradictory, or
underspecified project artifacts.

Freshness is not a historical log.
It is a practical check on whether the current durable context is still safe to
use.

Path examples below assume the default consuming-repo live project-doc surface
under `docs/`. A repo-local override may relocate those artifacts.

## Freshness states

- `current`: the active project context is specific enough and recent enough to
  execute from safely
- `stale`: the active context is likely drifting from reality and should be
  refreshed before meaningful execution continues
- `unknown`: there is not enough evidence to decide whether the context is
  current or stale

## Typical signs of `current`

- the active milestone is clear and still matches the intended work
- the session brief points to a real next action
- known blockers and risks still look relevant
- open questions reflect actual unresolved decisions rather than old history
- there is no obvious contradiction between the durable artifacts and the work
  being attempted

## Typical signs of `stale`

- milestone scope or acceptance no longer matches the work being discussed
- the next action is missing, obviously outdated, or no longer actionable
- blockers are resolved but still recorded as active, or missing even though
  they are now constraining work
- the project is repeatedly relying on chat reconstruction instead of durable
  context
- different artifacts contradict each other about scope, status, or next step
- a human decision has effectively been made but the durable artifacts still
  reflect the old assumption

## Typical signs of `unknown`

- the project has durable artifacts but they are too sparse to trust
- only part of the expected surface exists
- the repo or project has just been re-entered after a long gap
- there is not enough local evidence yet to mark the context as current

## Refresh rules

Refresh before meaningful execution when:
- freshness is `stale`
- freshness is `unknown` and the task is non-trivial
- the first serious blocker is actually ambiguity in the durable context
- multiple artifacts disagree about the active milestone or next move

Do not force a full refresh for every small action.
If a narrow correction can safely restore freshness, prefer that narrower
write-back.

## Minimum refresh expectation

A useful refresh should:
- restate the active milestone cleanly
- re-establish the next actionable step
- remove or rewrite stale blockers and assumptions
- promote real decisions into an explicit durable surface

Typical write-back targets:
- `docs/session-brief.md`
- `docs/current-milestone.md`
- `docs/open-questions.md`

## Relationship to `project-refresh`

Use `project-refresh` when freshness is stale, unknown, contradictory, or too
vague to execute from safely.

The goal is not to rewrite everything.
The goal is to restore enough durable clarity that execution can proceed
without leaning on chat memory.

# Session Brief

## Snapshot
- Project: `llm-os`
- Current stage: `Prototype`
- Active milestone: define the first minimal control-tower layer across
  projects
- Session contract: `project-refresh` plus `operating-model-update` when core
  files or operating surfaces are being changed
- Last updated: `2026-04-25`

## Project summary
`llm-os` now has the core first-cut pieces in place: template split, playbook,
external-skills boundary, freshness model, decisions log, lightweight human
input skills, repo initialization, Notion-first ideation guidance, and thin
Claude compatibility shims.

The repo-level stabilization and validation pass is accepted as complete enough
to advance. The main remaining gap is not whether the current surface basically
works. It is that there is still no strong, durable way to check whether
llm-os intent was fully met in validation without relying on human judgment.

The next highest-value slice is therefore the control tower: a minimal
cross-project visibility layer that helps with prioritization, stale-state
handling, and human decisions without creating a second execution source of
truth.

## Next action
Define the minimum viable control-tower layer, then test it against current
active projects without making Notion or portfolio tracking load-bearing for
execution.

## Blocking question
What is the minimum useful control-tower shape that improves visibility without
becoming a second PM system?

## Latest decisions
- `templates/` is the canonical reusable artifact layer.
- `docs/` is the live project-doc surface by default.
- `llm-os` uses `llm-os-docs/project/` as an explicit local project-doc
  override.
- `llm-os-docs/` is llm-os-specific explanation and deeper repo
  documentation.
- `llm-os-docs/background/` is non-default reference material.
- local repo instructions can override llm-os defaults and should declare those
  overrides explicitly.
- framework comparison belongs in `llm-os-docs/`, not in the live project-doc
  surface.
- `templates/AGENTS.md` plus `skills/repo-initialize/SKILL.md` are now the
  bootstrap path for bringing a consuming repo into the working model.
- before a repo exists, one canonical Notion page may be the live ideation and
  review surface; after repo creation, the repo becomes the execution source of
  truth and Notion becomes the summary and feedback surface.
- broad historical cleanup stays deferred until after the next bulk of work.
- the current validation pass is accepted as complete enough for now even
  though the checking method remains weak.
- the next highest-value slice is the control tower.

## Current risks
- there is still no durable, lightweight validation rubric for checking whether
  llm-os intent was fully satisfied in practice
- a control tower can easily become a second source of truth if the repo/Notion
  boundary is not kept explicit
- historical background docs still contain time-scoped analysis that can be
  mistaken for live source of truth if they are pulled into default context

## Expected output from this session
A minimal control-tower milestone definition with clear repo/Notion boundaries,
minimum project inputs, freshness handling, and a follow-on plan for improving
validation checking.

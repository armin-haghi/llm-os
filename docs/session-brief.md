# Session Brief

Use this doc to reload the current working context for `llm-os` in a few
minutes.

This doc does not replace `docs/current-milestone.md`.
Use the milestone doc for the broader multi-session target and acceptance
boundary. Use the session brief for the immediate slice of work, next action,
and most important live question inside that milestone.

## Snapshot
- Project: `llm-os`
- Current stage: `Prototype`
- Active milestone: stabilize the first-cut operating surface and self-host the
  repo docs cleanly
- Session contract: `project-refresh` plus `operating-model-update` when core
  files or operating surfaces are being changed
- Last updated: `2026-04-24`

## Project summary
`llm-os` now has the core first-cut pieces in place: template split, playbook,
external-skills boundary, freshness model, decisions log, and lightweight human
input skills.

This cleanup pass is separating the live project-doc surface from llm-os
explanatory material, moving deeper repo notes into `llm-os-docs/`, and
checking the full repo for remaining inconsistencies.

The main remaining risk is not missing theory. It is transitional or historical
documentation that still points at older structure.

## Next action
Run the consistency review after the docs cleanup, then decide whether to
validate llm-os on a real project before taking on more core slices.

## Blocking question
How aggressively should historical background analysis be rewritten now that the
core first-cut cleanup is materially complete?

## Latest decisions
- `templates/` is the canonical reusable artifact layer.
- `docs/` is the live project-doc surface by default.
- `llm-os-docs/` is llm-os-specific explanation and deeper repo
  documentation.
- `llm-os-docs/background/` is non-default reference material.
- local repo instructions can override llm-os defaults and should declare those
  overrides explicitly.
- llm-os should now self-host its own project docs instead of leaving the
  top-level `docs/*.md` files as placeholders.
- framework comparison belongs in `llm-os-docs/`, not in the live project-doc
  surface.

## Current risks
- historical background docs still contain time-scoped analysis that can be
  mistaken for live source of truth
- some older references still point at pre-split structure
- the repo now has a stronger first cut, but it still needs real-project
  validation before assuming the model is settled

## Expected output from this session
A repo cleanup pass that finishes the `llm-os-docs/` split, a current
consistency review in `docs/review-report.md`, and an explicit list of residual
gaps that remain after cleanup.

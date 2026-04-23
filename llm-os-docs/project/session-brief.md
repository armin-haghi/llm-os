# Session Brief

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
Close out the cleanup milestone, then define the first real-project validation
milestone and target repo.

## Blocking question
How aggressively should historical background analysis be rewritten now that the
core first-cut cleanup is materially complete?

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

## Current risks
- historical background docs still contain time-scoped analysis that can be
  mistaken for live source of truth
- some older references still point at pre-split structure
- the repo now has a stronger first cut, but it still needs real-project
  validation before assuming the model is settled

## Expected output from this session
A repo cleanup pass that removes duplicate guidance between `templates/`,
the consuming-repo `docs/` convention, and `llm-os-docs/`, plus a clearer next
step for real-project validation.

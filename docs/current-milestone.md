# Current Milestone

Use this doc to define the one milestone `llm-os` is actively trying to
complete.

This is the broader multi-session target, not the current session plan.
Use `docs/session-brief.md` for the immediate slice of work being taken against
this milestone.

## Snapshot
- Project: `llm-os`
- Stage: `Prototype`
- Milestone: stabilize the first-cut operating surface and self-host the repo
  docs cleanly
- Owner: human maintainer with agent support
- Status: `active`
- Last updated: `2026-04-24`

## Why this milestone matters
This milestone converts the repo from a strong conceptual core plus
transitional scaffolding into a coherent operating surface that can be used and
stress-tested on a real project.

If it succeeds:
- the repo’s own project docs stop acting like placeholders
- the first-cut operating model becomes internally consistent enough to test in
  real use
- remaining work becomes a bounded next-slice problem instead of general repo
  drift

Later work should largely wait for this because adding more slices on top of an
unclean base would hide the real gaps.

## In scope
- finish the first-cut core surfaces that were still missing or implied
- convert top-level `docs/*.md` from template placeholders into live llm-os
  project docs
- keep `templates/` as the canonical reusable template layer
- place deeper repo clarification docs in the right tier
- run a consistency check and record residual gaps durably

## Out of scope
- Notion control-tower design
- concurrency rules implementation
- stage-skill expansion
- machine-readable schemas beyond the minimum project overview input
- tool compatibility outputs
- broad historical rewrites of every background note

## Acceptance criteria
- the core operating layer includes the platform playbook, external-skills
  boundary, freshness model, and decisions log
- the lightweight human-input and human-topic skills exist and match the core
  model
- `templates/` is clearly canonical for reusable artifacts
- top-level `docs/*.md` contain live llm-os project state rather than template
  instructions
- deeper clarification docs are separated from background/reference docs
- `docs/review-report.md` records a current consistency review with explicit
  residual gaps

## Dependencies
- human decisions about doc-surface boundaries and cleanup sequencing
- time to reconcile the first-cut operating surface against older background
  notes
- willingness to leave some historical docs marked as historical instead of
  rewriting all of them immediately

## Blockers
- none currently
- residual risk remains around older background notes that still mention
  pre-cleanup structure

## Open questions to clarify during active sessions
- how aggressively should historical background analysis be rewritten now that
  the first-cut cleanup is materially complete?
- after this milestone closes, should the next validation step be a real
  project onboarding pass before more core expansion?

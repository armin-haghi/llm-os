# Decisions

This file records short, load-bearing decisions about the `llm-os` operating
model.

It is not a full history log.
Use it only for decisions that change how the system should be understood or
used later.

## When to record a decision

Record a decision here when it:
- changes the operating surface
- changes a core boundary or rule
- resolves an ambiguity that would otherwise be re-litigated
- affects how entry points, templates, skills, or write-back behavior should
  work

Do not record:
- routine edits
- one-off implementation choices that do not change the model
- temporary exploration notes
- general status updates

## Entry format

Keep entries short and durable.

### YYYY-MM-DD - [decision title]
- Status: active | superseded
- Decision: what was decided
- Why it matters: what this changes in practice
- Implication: what surfaces or behavior should follow from it
- Supersedes: older entry title if relevant

## Active decisions

### 2026-04-24 - Separate templates from repo docs
- Status: active
- Decision: `templates/` is the canonical template layer; `docs/` is the live
  project-doc surface by default for consuming repos; `llm-os-docs/project/`
  is the explicit live project-doc override for this repo; `llm-os-docs/` is
  llm-os-specific explanation; `llm-os-docs/background/` is non-default
  reference material
- Why it matters: agents should not have to load explanatory repo material just
  to find operational templates or live project state
- Implication: entry surfaces should point to `templates/` for reusable
  artifacts, treat `docs/` as the consuming-repo default, treat
  `llm-os-docs/project/` as this repo's live project state, and keep
  `llm-os-docs/background/` out of the default path
- Supersedes: none

### 2026-04-24 - Repo-local overrides beat llm-os defaults
- Status: active
- Decision: if a target repo needs to override llm-os defaults, such as the
  live project-doc location or other operating-surface rules, that override
  should be declared in the target repo's local `AGENTS.md`
- Why it matters: llm-os needs sensible defaults, but real repos must be able
  to declare bounded local deviations without forking the model
- Implication: agents should follow local repo instructions over generic llm-os
  assumptions when the repo states an explicit override
- Supersedes: none

### 2026-04-24 - llm-os uses an explicit local project-doc override
- Status: active
- Decision: this repo keeps its live llm-os project state under
  `llm-os-docs/project/*.md` while `docs/` remains the default consuming-repo
  convention and `templates/` remains the canonical reusable template layer
- Why it matters: the repo should follow its own operating model instead of
  blurring the difference between template/default repo surfaces and llm-os
  repo-specific documentation
- Implication: `AGENTS.md` and repo-local read paths should point to
  `llm-os-docs/project/`, while historical analysis stays in
  `llm-os-docs/background/` unless promoted
- Supersedes: none

### 2026-04-24 - Notion may be the pre-repo ideation surface
- Status: active
- Decision: before a repo exists, one canonical Notion page may serve as the
  live ideation and review surface; once a repo exists and active build starts,
  the repo becomes the execution source of truth and Notion becomes the
  summary, review, and feedback surface
- Why it matters: early-stage work often needs comments and lightweight review
  before a repo exists, but stale Notion pages become harmful when they compete
  with repo docs during build
- Implication: pre-repo skills may write to one canonical Notion page; after
  repo creation, durable execution state should move into repo docs and Notion
  should stop acting as a second build surface
- Supersedes: none

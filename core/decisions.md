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
  project-doc surface by default; `llm-os-docs/` is llm-os-specific explanation;
  `llm-os-docs/background/` is non-default reference material
- Why it matters: agents should not have to load explanatory repo material just
  to find operational templates or live project state
- Implication: entry surfaces should point to `templates/` for reusable
  artifacts, treat `docs/` as live project state by default, and keep
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

### 2026-04-24 - llm-os self-hosts project state in docs
- Status: active
- Decision: this repo now uses top-level `docs/*.md` as live llm-os project
  state while `templates/` remains the canonical reusable template layer
- Why it matters: the repo should follow its own operating model instead of
  leaving the project-doc surface as placeholder text
- Implication: top-level `docs/*.md` should contain current llm-os project
  state, while historical analysis stays in `llm-os-docs/background/` unless
  promoted
- Supersedes: none

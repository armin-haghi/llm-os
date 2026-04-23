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
- Decision: `templates/` is the canonical template layer; `docs/` is repo
  documentation and deeper clarification; `docs/background/` is non-default
  reference material
- Why it matters: agents should not have to load repo documentation just to
  find operational templates
- Implication: entry surfaces should point to `templates/` for reusable
  artifacts and keep `docs/background/` out of the default path
- Supersedes: none

### 2026-04-24 - Keep agent-action surfaces outside docs by default
- Status: active
- Decision: normal agent work should route through `AGENTS.md`, `core/`,
  `skills/`, and `templates/`, not `docs/`
- Why it matters: `docs/` is for clarification and repo documentation, not the
  default action surface
- Implication: new operational behaviors should avoid making `docs/` the
  primary control plane unless the repo explicitly requires it
- Supersedes: none

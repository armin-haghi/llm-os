# Project Spine

## What
`llm-os` is a reusable operating standard for agent-driven product work that
gives humans and agents a bounded lifecycle model, durable project memory, and
small-context execution rules across tools.

## Why
It exists to reduce chat drift and make serious project work durable,
reviewable, and reusable instead of reconstructed from scratch in each tool.

Right now the immediate need is to turn the first-cut operating model into a
coherent self-hosting repo surface that can support a first real project
without re-deciding the basics every session.

## Who
- Primary users: humans operating serious project work with coding agents and
  chat-style tools
- Operators: the repo maintainer and any agent working inside the `llm-os`
  operating surface
- Internal owner: the maintainer shaping the operating model and deciding which
  patterns become core

## Constraints
- Must stay lightweight and avoid turning into a full PM framework
- Must preserve the human as the decision endpoint
- Must keep core operating behavior separate from capability-specific logic
- Must work across multiple entry points without fragmenting the model
- Must minimize default context load
- Must clean up the repo’s own self-hosting surface without reopening every
  earlier design decision

## Success criteria
- A first real project can be onboarded without major ambiguity about read
  paths, write-back, template usage, or agent/human boundaries
- The repo’s own live project-doc surface under `llm-os-docs/project/`
  reflects current state cleanly without being confused with the consuming-repo
  `docs/` convention
- Core files, skills, templates, and project docs stay internally consistent
- Remaining gaps are explicit and bounded to future slices rather than hidden in
  drift

## Current milestone
- Current stage: `Prototype`
- Active milestone: see `llm-os-docs/project/current-milestone.md`
- If this milestone succeeds, the first-cut operating surface should be stable
  enough to validate on a real project instead of continuing as repo-only
  theory

## Canonical links
- Repo root
- `AGENTS.md`
- `README.md`
- `core/operating-model.md`
- `core/agent-contracts.md`
- `core/platform-playbook.md`
- `core/decisions.md`
- `llm-os-docs/project/current-milestone.md`
- `llm-os-docs/project/open-questions.md`
- `llm-os-docs/project/session-brief.md`
- `llm-os-docs/project/review-report.md`

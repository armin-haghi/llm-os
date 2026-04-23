---
name: repo-initialize
description: Initialize or retrofit a consuming repo into the llm-os working model.
---

# Repo Initialize

Use this skill when a repo does not yet have the minimum `llm-os` operating
surface in place, including an existing repo that has work and docs already but
does not yet follow the model.

## Goal

Bring a repo to the minimum working model so an agent can pick it up repo-first
without depending on Notion or prior chat context.

## Start with audit, not scaffolding

For an existing repo, inspect before creating anything.

Check:
- current entry surfaces such as `AGENTS.md`, `README.md`, `ASSISTANT.md`, or `CLAUDE.md`
- current live docs such as `docs/`, `planning/`, `notes/`, `specs/`, or similar folders
- whether the repo already has a durable milestone doc, session handoff, or project summary

Map what already exists to the canonical artifacts:
- `project-spine.md`
- `current-milestone.md`
- `open-questions.md`
- `session-brief.md`
- `review-report.md`
- `project-overview.yaml`

## Decide the live project-doc surface

Default to `docs/`.

Keep an existing non-default location only when moving it would create more
confusion than clarity right now.

If keeping a non-default location:
- declare it explicitly in the repo's local `AGENTS.md`
- treat that location as the live project-doc surface
- do not create a second parallel `docs/` surface just because it is the default

## Create only what is missing

For a new or empty repo, create:
1. root `AGENTS.md` from `templates/AGENTS.md`
2. `docs/project-spine.md` from `templates/project-spine.md`
3. `docs/current-milestone.md` from `templates/current-milestone.md`
4. `docs/open-questions.md` from `templates/open-questions.md`
5. `docs/session-brief.md` from `templates/session-brief.md`
6. `docs/review-report.md` from `templates/review-report.md`
7. `project-overview.yaml` from `templates/project-overview.yaml`

For an existing repo:
1. create root `AGENTS.md` if missing
2. keep and reuse existing docs when they already serve a canonical role
3. create only missing canonical artifacts
4. migrate or rewrite weak docs only when needed to remove ambiguity

Do not duplicate an existing usable doc just to match the default filenames.
Prefer one live surface with clear mapping over two partially overlapping ones.

## Normalize existing docs when needed

If a repo already has planning or handoff docs:
- treat the best current artifact as the starting source
- rewrite or condense it into the canonical artifact shape when needed
- preserve durable content, but remove duplicate or competing summaries

Typical examples:
- a roadmap or sprint note can become `current-milestone.md`
- a handoff note can become `session-brief.md`
- a project README or spec can seed `project-spine.md`
- an issue list or TODO note can seed `open-questions.md`

## Fill the minimum required content

Do not leave the repo as a pure empty scaffold or as a retrofit with only file
renames and no usable content.
Fill at least:

- the live `project-spine.md`
  - what
  - why
  - who
  - constraints
  - success criteria
  - canonical links
- the live `current-milestone.md`
  - snapshot
  - why this milestone matters
  - in scope
  - out of scope
  - acceptance criteria
- the live `session-brief.md`
  - snapshot
  - project summary
  - next action
  - blocking question
  - expected output from this session
- `project-overview.yaml`
  - project
  - stage
  - active_milestone
  - freshness
  - blocker
  - next_action
  - commercial_signal

The live `open-questions.md` and `review-report.md` may start sparse, but they
should exist.

## Repo-local overrides

If the repo needs a non-default live project-doc location or any other
llm-os override, declare it explicitly in the repo's local `AGENTS.md`.

Do not invent overrides without a concrete repo reason.

## Minimum readiness check

Initialization is complete only when:

1. root `AGENTS.md` exists and points to the live project-doc surface
2. all five canonical project docs exist under the live project-doc surface or are explicitly mapped there without parallel duplicates
3. the active milestone is specific enough to execute against
4. the session brief points to a real next action
5. `project-overview.yaml` exists with current values
6. the repo no longer requires Notion just to begin serious work
7. the repo does not have two competing project-doc surfaces that say different things

## Follow-on

After initialization, the next session should normally use:

1. `existing-project` if the docs are now in place and work can begin
2. `project-refresh` if the initialized docs are still vague or stale

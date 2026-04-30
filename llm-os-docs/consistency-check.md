# Consistency Check

Status: active

This note defines the lightweight check that prevents repo, Notion, and run
handoff drift.

Use it during project sweeps, selected-project orchestration, and any serious
session that relies on both Notion and repo docs.

## Purpose

The check exists to prevent these failure modes:

- a completed Agent Run Queue record being mistaken for latest state
- a Notion Project Control Tower record lagging behind repo docs
- repo docs being updated without Notion portfolio state being refreshed
- a project being marked current while it is missing required `llm-os`
  compatibility fields
- an agent relying on chat memory instead of canonical repo/Notion surfaces

## Required inputs

For each repo-backed project, read:

1. Project Control Tower record
2. relevant Agent Run Queue records, especially ready, in-flight,
   waiting-human, blocked, and recent done records
3. repo `project-overview.yaml`
4. repo live project docs, usually current milestone and session brief, only
   when the overview is missing, stale, or contradictory
5. current `llm-os` standard from `llm-os-docs/version-log.md`

For pre-repo projects, read:

1. Project Control Tower record
2. canonical Notion page from the `Notion Page` field
3. relevant Agent Run Queue records

## Alignment states

Classify each project as one of:

- `aligned`
  - repo overview, live project docs, and Notion record agree on active
    milestone, blocker, next action, next decision, freshness, and last checked
    state
- `repo-newer-than-notion`
  - repo docs, repo commits, or repo overview contain newer project state than
    Notion
- `notion-newer-than-repo`
  - Notion claims a milestone, decision, or run result that has not been written
    back to repo docs
- `unknown`
  - required repo or Notion context is unavailable

## Rules

- Repo docs decide execution state once a repo exists.
- Notion decides portfolio state, run dispatch, blockers, and human decisions.
- Completed run records are historical unless they explicitly say they are the
  latest state as of a commit.
- If a completed run references a commit that is behind repo head, preserve the
  run as history and update its handoff or create a follow-on run.
- Do not invent milestone intent from Notion when repo docs disagree.
- Do not update repo docs from Notion unless the run or user explicitly asks for
  that write-back and the change is safe.

## Compatibility check

For each repo-backed project, compare `project-overview.yaml` against the
current standard in `llm-os-docs/version-log.md`.

Required compatibility fields:

- `llm_os_version`
- `llm_os_profile`
- `llm_os_last_checked`
- `llm_os_update_needed`
- `llm_os_update_reason`

Set compatibility state as:

- `current`
  - project version matches the current standard and no required fields are
    missing
- `update-needed`
  - project version is older than the current standard or required fields are
    missing
- `unknown`
  - repo state or version metadata is unavailable

Prefer one bounded migration run per project over many small migration tasks.

## Write-back behavior

When drift is found:

- update Project Control Tower for portfolio/run state drift
- update Agent Run Queue for stale or misleading run state
- update repo `project-overview.yaml` only when safe and explicitly within the
  sweep or migration scope
- create a bounded migration run when repo updates are needed but not safe to do
  immediately

## Human summary

A project sweep should report:

- source-of-truth alignment state
- LLM-OS compatibility state
- update needed and why
- blocker or human decision, if any
- next recommended run

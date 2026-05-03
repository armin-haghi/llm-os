# LLM-OS Version Log

This file tracks compatibility-impacting changes to `llm-os`.

Use this log to decide whether a consuming repo needs a migration or refresh.
Do not add an entry for wording cleanup, background notes, or internal docs that
do not change how a consuming project should be structured or operated.

## Current standard

- Current version: `0.4`
- Current profile: `repo-backed-orchestration`
- Date: `2026-05-03`

## Version rules

Increment `llm_os_version` only when a consuming project would need to change one
or more of:

- root `AGENTS.md` or equivalent project entrypoint
- live project docs or read paths
- `project-overview.yaml`
- Agent Run Queue usage
- Project Control Tower fields
- orchestration prompts or required sweep behavior
- write-back or escalation behavior

Do not increment for:

- wording cleanup
- examples
- background notes
- historical analysis
- internal-only explanation that does not affect consuming repos

## 0.4 — Repo state and review-agent tracking

Date: `2026-05-03`

Impact: repo-backed projects should expose the last branch/commit known to the
control layer and whether a review or refresh agent is needed after repo changes.

Migration required: yes, for repo-backed projects that participate in Project
Control Tower or Agent Run Queue orchestration.

Affected surfaces:

- `templates/project-overview.yaml`
- `project-overview.yaml` in each consuming repo
- Project Control Tower fields
- Agent Run Queue closeout behavior
- project sweep behavior

Migration checklist:

- Add `repo_branch` to the repo's `project-overview.yaml`.
- Add `repo_latest_commit`.
- Add `repo_state_checked`.
- Add `repo_review_needed` as `yes`, `no`, or `unknown`.
- Add `repo_review_reason`.
- Add `repo_review_agent` as `review-gate`, `project-refresh`, or `none`.
- When a run changes repo files, update these fields before closing the run.
- If a coding/build agent changed repo state, default `repo_review_needed` to
  `yes` unless the run itself was a review-only run.
- During project sweep, compare the recorded commit against the current repo
  head and surface projects that need review or refresh.

## 0.3 — Consistency and compatibility tracking

Date: `2026-04-28`

Impact: consuming repos should expose their LLM-OS compatibility state so project
sweeps can detect whether repo docs, Notion records, and agent handoffs are
aligned.

Migration required: yes, for repos that participate in Project Control Tower or
Agent Run Queue orchestration.

Affected surfaces:

- `templates/project-overview.yaml`
- `project-overview.yaml` in each consuming repo
- `orchestration/README.md`
- `orchestration/prompts/project-sweep.md`
- Project Control Tower fields

Migration checklist:

- Add `llm_os_version` to the repo's `project-overview.yaml`.
- Add `llm_os_profile` to distinguish repo-backed, Notion-only, or hybrid use.
- Add `llm_os_last_checked` with the last sweep or migration-check date.
- Add `llm_os_update_needed` as `yes`, `no`, or `unknown`.
- Add `llm_os_update_reason` with the specific missing field, stale entrypoint,
  or migration reason.
- During project sweep, compare each project against the current standard in
  this file.

## 0.2 — Control Tower and Agent Run Queue

Date: `2026-04-25`

Impact: introduced the minimal cross-project control layer and bounded run queue.

Migration required: yes, for active projects that should be visible in the
Project Control Tower or dispatched through the Agent Run Queue.

Affected surfaces:

- Project Control Tower
- Agent Run Queue
- `templates/project-overview.yaml`
- `templates/agent-run.yaml`
- `llm-os-docs/control-tower.md`

## 0.1 — Repo-backed project operating surface

Date: `2026-04-24`

Impact: established root entrypoint, repo-local project docs, active milestone,
open questions, session brief, and review report as the basic operating surface.

Migration required: yes, for repos adopting `llm-os` for the first time.

Affected surfaces:

- root `AGENTS.md`
- `docs/project-spine.md`
- `docs/current-milestone.md`
- `docs/open-questions.md`
- `docs/session-brief.md`
- `docs/review-report.md`

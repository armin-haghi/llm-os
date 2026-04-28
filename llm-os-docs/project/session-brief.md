# Session Brief

## Snapshot
- Project: `llm-os`
- Current stage: `Prototype`
- Active milestone: test and harden the minimal control-tower, Agent Run Queue,
  and shared orchestration path across active projects
- Session contract: `orchestration` plus `operating-model-update` when core
  files or operating surfaces are being changed
- Last updated: `2026-04-28`

## Project summary

`llm-os` now has the core operating surface in place: root `AGENTS.md`, core
operating docs, templates, live project docs under `llm-os-docs/project/`, the
Project Control Tower, the Agent Run Queue, orchestration prompts, and an
orchestrator skill.

The first control-tower and Agent Run Queue shape has been defined. The next
highest-value work is to test whether it actually drives parallel product work
without forcing the human to reconstruct thread context or creating a second
execution truth in Notion.

The shared orchestration path is the human-facing front door for this layer. It
should support two flows:
- project sweep: refresh project/control-tower/run state and surface real human
  decisions
- selected-project work: choose or create one bounded run, execute or dispatch
  it, and write back before closing

## Next action

Run a project sweep using the shared orchestration path, then start one selected
project through the Agent Run Queue and verify that the run can be completed
with durable write-back.

## Blocking question

What is the smallest durable consistency check that prevents Notion/repo drift
without adding bureaucracy?

## Latest decisions
- `templates/` is the canonical reusable artifact layer.
- `docs/` is the live project-doc surface by default for consuming repos.
- `llm-os` uses `llm-os-docs/project/` as an explicit local project-doc
  override.
- `llm-os-docs/background/` is non-default reference material.
- local repo instructions can override llm-os defaults and should declare those
  overrides explicitly.
- before a repo exists, one canonical Notion page may be the live ideation and
  review surface.
- after repo creation, the repo becomes the execution source of truth and
  Notion becomes the portfolio, summary, run-dispatch, blocker, and feedback
  surface.
- the Project Control Tower should track one current project record per
  project, not one record per milestone or session.
- the Agent Run Queue should track bounded agent sessions and handoffs, not a
  backlog of tiny tasks.
- `orchestration/README.md` is the shared cross-interface path for project
  sweeps and selected-project work.
- `AGENTS.md` now routes orchestration requests to the shared orchestration
  path.

## Current risks
- completed run handoffs can become stale if follow-on commits are not reflected
  in Notion
- Notion views can silently hide relevant work if their filters differ from
  repo-defined semantics
- the Agent Run Queue can become a backlog if runs are too small, vague, or
  numerous
- agents can regress to chat-memory reasoning if they do not start from
  repo/Notion freshness checks
- there is still no durable, lightweight validation rubric for checking whether
  llm-os intent was fully satisfied in practice

## Expected output from this session

A validated control-tower plus Agent Run Queue path, with source-of-truth drift
identified and repaired, and a follow-on consistency check that can be reused in
future project sweeps.

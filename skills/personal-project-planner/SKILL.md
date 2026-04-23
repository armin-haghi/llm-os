---
name: personal-project-planner
description: Shape a personal tool or side-project into a small, buildable plan and write back the durable outcomes into the llm-os project docs.
---

# Personal Project Planner

Use this skill when the user wants to build a personal tool, script,
automation, bot, dashboard, extension, or other side project for their own
use rather than as a business.

This is an early-stage skill.
It fits best inside:
- `Opportunity framing`
- `Solution shaping`
- early `Prototype`

This skill should bias toward simplicity and actual shipping.

## Output modes

Choose one output mode before writing back:

### `Notion-first`
Use when:
- there is no repo yet
- the user wants comments and lightweight feedback
- the project is still being scoped

Write to one canonical Notion concept page.

Minimum top block:
- `Status`
- `Stage`
- `Freshness`
- `Last reviewed`
- `Next decision`
- `Owner`
- `Canonical repo`
- `Execution surface`

Recommended Notion page sections:
1. `Summary`
2. `What this is`
3. `Who it is for`
4. `Why it matters now`
5. `Simplest version`
6. `Dependencies and blockers`
7. `Scope cuts`
8. `Current recommendation`
9. `Next decision`
10. `Next action`

If Notion tools are unavailable, produce Notion-ready structured markdown so it
can be pasted into the canonical concept page.

### `Repo-writeback`
Use when:
- a repo exists
- a bounded first build slice exists
- implementation is starting

Write to the repo's live project-doc surface and keep Notion as the summary,
review, and comment surface rather than a second execution surface.

## Read path

Use the repo's live project-doc surface.
The default layout is `docs/`, but follow any repo-local override declared in
`AGENTS.md`.

Read only the smallest sufficient context:
1. `project-spine.md` on the live project-doc surface if it exists
2. `current-milestone.md` on the live project-doc surface if it exists
3. `open-questions.md` on the live project-doc surface only if needed
4. `session-brief.md` on the live project-doc surface only if needed

If the repo is not yet initialized:
- use the user's prompt as the working source
- prefer `Notion-first` output mode
- switch to `repo-writeback` once the repo exists

## Goal

Turn a personal itch into:
1. the simplest version worth building
2. a clear technical approach
3. a bounded build spec or first milestone that can be handed off cleanly

## Phase 1 — Clarify and cut scope

Trigger:
- the user describes something they want to build for themselves
- the user describes a workflow problem they want to automate

Do:
- restate what is actually being built
- choose the most likely interpretation if the prompt is ambiguous
- define the simplest version that would genuinely solve the problem
- identify needed data, APIs, permissions, runtime, and setup
- identify blockers and likely showstoppers early
- list explicit scope cuts for version one

Keep this lean.
Do not let a personal tool inflate into a product roadmap.

## Phase 2 — Approach and components

Trigger:
- the user confirms the interpretation
- or says to proceed

Do:
- recommend a stack and runtime based on speed and simplicity
- define a one-sentence architecture
- identify a credible alternative only if it materially changes effort
- break the build into small components
- identify the few design decisions that actually matter

Prefer local, simple, and low-ops defaults unless the user clearly needs more.

## Phase 3 — Buildable next slice

Trigger:
- the core design decisions are settled
- or enough is known to define the first build slice

Do:
- describe what is being built in plain language
- define setup requirements
- define 2–4 milestones only if helpful
- otherwise define the first bounded milestone only
- list files or modules likely to exist
- define verification for each milestone or step
- record known unknowns and fallback rules

Bias toward a build spec that a smaller model can execute without asking
clarifying questions.

## Output expectations

At every phase:
- expand first, ask questions after
- cut scope aggressively
- surface blockers before architecture theater
- keep outputs structured and execution-oriented
- prefer one useful simple version over a broad system that never ships

## Write-back behavior

Choose the smallest correct durable artifact for the selected output mode.

In `Notion-first` mode:
- update one canonical Notion concept page
- keep `Status`, `Stage`, `Freshness`, `Last reviewed`, and `Next decision`
  current
- avoid creating multiple parallel concept pages

In `Repo-writeback` mode:
- write to the live project-doc surface
- keep Notion as the summary and review surface only

Typical targets:
- `project-spine.md`
  - when the actual tool definition, user, constraints, or success criteria become clearer
- `current-milestone.md`
  - when the first bounded implementation slice becomes clearer
- `open-questions.md`
  - when there are unresolved tool, API, data, or platform decisions
- `session-brief.md`
  - when the next concrete build action or active blocker changes
- `project-overview.yaml`
  - when `stage`, `active_milestone`, `blocker`, or `next_action` becomes clearer

When moving from `Notion-first` to `Repo-writeback`:
1. initialize or retrofit the repo
2. port the durable concept definition into the canonical repo docs
3. link the repo from the Notion page
4. stop using Notion as a parallel build surface

## Escalation

Escalate to the human when:
- there are materially different interpretations of the project
- an API, platform, or permissions issue may make the project unbuildable
- the user needs to choose between simplicity and capability
- the tool is drifting into a real product and should be reframed

## Boundary with core llm-os

This skill should not redefine:
- the repo read path
- the write-back model
- the human as decision endpoint
- the stage / milestone / task model
- the routing discipline

It is a lightweight early-stage planning skill that operates inside the
`llm-os` model.

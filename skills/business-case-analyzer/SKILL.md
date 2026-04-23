---
name: business-case-analyzer
description: Analyze a business or product idea through opportunity framing and solution shaping, then write back the durable outcomes into the llm-os project docs.
---

# Business Case Analyzer

Use this skill when the user has a business idea, product concept, startup
thesis, feature set, or commercial opportunity they want expanded,
pressure-tested, and shaped into a buildable direction.

This is an early-stage skill.
It fits best inside:
- `Opportunity framing`
- `Solution shaping`

It is not the core operating model.
It plugs into `llm-os` and should write its outcomes back into the canonical
project docs.

## Output modes

Choose one output mode before writing back:

### `Notion-first`
Use when:
- there is no repo yet
- the user wants comments and feedback before build
- the concept is still being shaped in `Opportunity framing` or `Solution shaping`

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
3. `Who can pay`
4. `Value delivered`
5. `Market and alternatives`
6. `Key assumptions`
7. `Key risks`
8. `Current recommendation`
9. `Next decision`
10. `Next action`

Prefer updating the same page over creating a new page for every iteration.

If Notion tools are unavailable, produce Notion-ready structured markdown so it
can be pasted into the canonical concept page.

### `Repo-writeback`
Use when:
- a repo exists
- the project has a bounded first milestone
- active build is starting or already underway

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

Turn a short business description into:
1. a sharper opportunity view
2. a clearer system and go-to-market shape
3. a bounded next milestone that can actually be executed

Do not stop at brainstorm prose.
The output should improve project clarity and reduce ambiguity.

## Phase 1 — Opportunity framing

Trigger:
- a short business idea
- a product concept
- a startup thesis
- a request to analyze whether an idea is worth building

Do:
- identify who can pay
- identify what value is delivered and what cost of inaction exists
- size the market roughly with reasoning
- identify competitors, substitutes, and structural constraints
- identify the distinct product components and which are differentiating
- identify the main commercial and execution risks
- make the load-bearing assumptions explicit

Questions at the end should be the smallest set that most changes the analysis.
Lead with synthesis first.

## Phase 2 — Solution shaping

Trigger:
- the user responds to Phase 1
- or says to go deeper

Do:
- break the concept into components
- define what each component does and does not do
- note key technical and product tradeoffs
- identify integration points and major dependencies
- identify the first credible go-to-market path
- compile open design and business decisions

Keep this stage bounded.
Do not expand into an unprioritized product wish list.

## Phase 3 — Buildable next slice

Trigger:
- the main design questions have been answered
- or enough assumptions are stable to define a first bounded milestone

Do:
- produce a system overview in plain language
- define 3–6 milestones only if the user explicitly wants a fuller roadmap
- otherwise define the first bounded milestone only
- make tasks specific and verifiable
- name known unknowns and fallback rules

Bias toward a bounded first milestone over a long build memo.

## Output expectations

At every phase:
- synthesize before asking questions
- surface the hard bet explicitly
- distinguish assumptions from facts
- separate commercial risk, product risk, technical risk, and distribution risk
- keep outputs structured and durable, not chatty

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
  - when the project definition, buyer, value proposition, constraints, or success criteria become clearer
- `current-milestone.md`
  - when the first bounded milestone, scope, acceptance criteria, or stage framing become clearer
- `open-questions.md`
  - when the analysis surfaces unresolved business, product, or GTM decisions
- `session-brief.md`
  - when the immediate next action or active risk changes
- `project-overview.yaml`
  - when `stage`, `active_milestone`, `blocker`, `next_action`, or `commercial_signal` becomes clearer

Do not duplicate the same idea analysis across multiple files unless the repo
really needs that duplication.

When moving from `Notion-first` to `Repo-writeback`:
1. initialize or retrofit the repo
2. port the durable concept definition into the canonical repo docs
3. link the repo from the Notion page
4. stop using Notion as a parallel build surface

## Escalation

Escalate to the human when:
- the business depends on a real risk-acceptance choice
- prioritization between materially different directions is required
- the buyer, pricing logic, or distribution strategy cannot be narrowed safely
- the idea is still too ambiguous to produce a bounded milestone

## Boundary with core llm-os

This skill should not redefine:
- the repo read path
- the write-back model
- the human as decision endpoint
- the stage / milestone / task model
- the routing discipline

It is an early-stage shaping skill that operates inside the `llm-os` model.

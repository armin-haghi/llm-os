# Portable Ideation and Status Surfaces

Status: active

Compatibility note: this file keeps its historical path for now, but the
operating concept is no longer `Notion-first`. Do not infer that Notion is the
canonical project surface.

This note defines the lightweight `llm-os` pattern for early-stage work when a
repo does not exist yet and a status/review surface is the easiest place to
review, comment, and iterate. That surface may be Notion, Confluence, markdown
files, a project tracker, or another durable workspace.

This is not the control-tower design.
It is a minimal pre-repo or early-shaping review pattern.

## Purpose

Use one canonical status surface for a concept when:
- there is no repo yet
- the work is still in `Opportunity framing` or `Solution shaping`
- the human wants comments and lightweight feedback loops before build starts

The status surface is an implementation detail. The operating contract is:
- make current state durable
- keep the next decision visible
- avoid stale parallel pages
- preserve a clear transition into repo-backed execution when a repo exists

Once a repo exists and active build begins, the repo becomes the execution
source of truth. The status surface remains useful for portfolio summaries,
review, comments, run dispatch, and human decisions.

## One-surface rule

Use one canonical status page, document, or record per concept.

Do not create a new page for every iteration, expansion, or feedback cycle.
Keep the same surface live and update:
- status
- stage
- freshness
- last reviewed
- next decision

Child pages or linked docs are allowed only when they clearly reduce confusion.
Examples:
- a research appendix
- a technical deep-dive
- a build-readiness note

Comments should stay on the canonical concept surface whenever possible.

## Minimal fields

Every pre-repo concept surface should carry:

- `Status`
  - `idea`
  - `shaping`
  - `build-ready`
  - `active-build`
  - `parked`
  - `archived`
- `Stage`
  - one canonical `llm-os` stage
- `Freshness`
  - `current`
  - `stale`
  - `unknown`
- `Last reviewed`
- `Next decision`
- `Owner`
- `Canonical repo`
  - blank until a repo exists
- `Execution surface`
  - the canonical status surface before a repo exists
  - `repo` once active build starts

These can live as database properties, document metadata, frontmatter, a small
summary block, or a tracker row.

## Recommended structure

The body should stay compact and decision-friendly.

Recommended sections:

1. `Summary`
2. `What this is`
3. `Who it is for`
4. `Why it matters now`
5. `Value / outcome hypothesis`
6. `Key assumptions`
7. `Key risks`
8. `Current recommendation`
9. `Next decision`
10. `Next action`
11. `Links`

Optional sections:
- `Competitors / alternatives`
- `Component breakdown`
- `Go-to-market angle`
- `Technical constraints`
- `Open questions`

## Freshness and staleness

The goal is to stop project/status surfaces from filling up with records that
still look live even though nobody is actively shaping them.

Mark a surface `current` only when:
- it has been reviewed recently
- the `Next decision` is still real
- the recommendation still reflects the current thinking

Mark a surface `stale` when:
- it has not been reviewed recently
- the next decision is no longer clear
- the concept changed elsewhere and the surface was not updated

Mark a surface `parked` when:
- the concept is still interesting
- but no active shaping or build work is happening now

Mark a surface `archived` when:
- the concept is dead
- the surface has been superseded by another canonical surface
- or the project has moved fully into a different durable surface

Recommended practical default:
- review active `idea`, `shaping`, and `build-ready` surfaces at least every 2 weeks
- if not reviewed, set `Freshness` to `stale`
- if no active intent remains, move `Status` to `parked` or `archived`

## Transition to repo

Move from a status-surface-led pattern to repo-backed execution when:
- the concept is `build-ready`
- there is a real first milestone to execute
- implementation details need durable versioned write-back

At that point:
1. initialize or retrofit the repo with `repo-initialize`
2. create local `AGENTS.md`
3. create the canonical repo docs
4. port the durable subset of the concept into:
   - `project-spine.md`
   - `current-milestone.md`
   - `open-questions.md`
   - `session-brief.md`
   - `project-overview.yaml`
5. link the repo from the status surface
6. switch `Execution surface` from the status surface to `repo`

After that transition:
- repo docs are the execution source of truth
- the external status surface is summary, review, comment, run-dispatch, and human-decision support

## Comment-friendly review

A status surface is preferred early when the main need is:
- comments
- directional feedback
- rough shaping
- collaborative critique

GitHub or another versioned repo is better later for:
- build artifacts
- reviewed code and versioned changes
- milestone evidence tied to implementation

## Consistency rule

Before a repo exists:
- one canonical status surface may be the live working surface

After a repo exists:
- the repo becomes the execution source of truth
- the status surface should not become a second competing build surface

This is the main rule that keeps project tracking useful without letting it
become stale parallel documentation.

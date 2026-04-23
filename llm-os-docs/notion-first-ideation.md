# Notion-First Ideation

Status: active

This note defines the lightweight `llm-os` pattern for early-stage work when a
repo does not exist yet and Notion is the easier place to review, comment, and
iterate.

This is not the Notion control-tower design.
It is a minimal pre-repo review surface.

## Purpose

Use a single Notion page as the live ideation surface when:
- there is no repo yet
- the work is still in `Opportunity framing` or `Solution shaping`
- the user wants comments and lightweight feedback loops before build starts

Once a repo exists and active build begins, the repo becomes the execution
source of truth.
Notion remains the summary, review, and feedback surface.

## One-page rule

Use one canonical Notion page per concept.

Do not create a new page for every iteration, expansion, or feedback cycle.
Keep the same page live and update:
- status
- stage
- freshness
- last reviewed
- next decision

Child pages are allowed only when they clearly reduce confusion.
Examples:
- a research appendix
- a technical deep-dive
- a build-readiness note

Comments should stay on the canonical concept page whenever possible.

## Minimal properties

Every pre-repo concept page should carry:

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
  - `Notion` before a repo exists
  - `repo` once active build starts

These can live as database properties or as a small summary block at the top of
the page if no database exists yet.

## Recommended page structure

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

The goal is to stop Notion from filling up with pages that still look live even
though nobody is actively shaping them.

Mark a page `current` only when:
- it has been reviewed recently
- the `Next decision` is still real
- the recommendation still reflects the current thinking

Mark a page `stale` when:
- it has not been reviewed recently
- the next decision is no longer clear
- the concept changed elsewhere and the page was not updated

Mark a page `parked` when:
- the concept is still interesting
- but no active shaping or build work is happening now

Mark a page `archived` when:
- the concept is dead
- the page has been superseded by another canonical page
- or the project has moved fully into a different durable surface

Recommended practical default:
- review active `idea`, `shaping`, and `build-ready` pages at least every 2 weeks
- if not reviewed, set `Freshness` to `stale`
- if no active intent remains, move `Status` to `parked` or `archived`

## Transition to repo

Move from `Notion-first` to `repo-first` when:
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
5. add the repo link back to the Notion page
6. switch `Execution surface` on the Notion page from `Notion` to `repo`

After that transition:
- repo docs are the execution source of truth
- Notion is the summary, review, and comment surface

## Comment-friendly review

Notion is the preferred early-stage review surface when the main need is:
- comments
- directional feedback
- rough shaping
- collaborative critique

GitHub is better later for:
- build artifacts
- reviewed code and versioned changes
- milestone evidence tied to implementation

## Consistency rule

Before a repo exists:
- one canonical Notion page may be the live working surface

After a repo exists:
- the repo becomes the execution source of truth
- Notion should not become a second competing build surface

This is the main rule that keeps Notion useful without letting it become stale
parallel documentation.

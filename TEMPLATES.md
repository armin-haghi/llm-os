# Document Templates

Standard templates for each artifact type in the workflow.

---

## Project Spine

This is the stable, long-lived context for a project. Copy into `docs/project-spine.md`.

```
# Project Spine

## What this project is

## Why it matters

## Who it is for

## Current goal

## Success criteria

## Non-negotiable constraints

## Current architecture or operating model

## Key decisions so far

## Current workstreams

## Top open questions

## Canonical docs
- `docs/current-milestone.md`
- `docs/decision-log.md`
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- corresponding Notion milestone page
```

---

## Decision Log

Track decisions in `docs/decision-log.md`. Add a new section for each decision.

```
## YYYY-MM-DD — Decision title

### Context

### Decision

### Why

### Tradeoffs

### Implications

### Revisit when
```

---

## Handoff to Builder

For active implementation work. Use in `docs/handoffs/active-build.md`.

```
# Handoff to Builder

## Metadata
- Project:
- Milestone:
- Owner:
- GitHub issue:
- Related Notion milestone:

## Objective

## User / business context

## Proposed solution

## Constraints

## Assumptions

## Relevant decisions

## Files to create or change

## Acceptance criteria

## Tests / validation

## Non-goals

## Supporting docs to read
1. `docs/project-spine.md`
2. `docs/decision-log.md`
3. additional docs:

## Open questions
```

---

## Milestone Plan

For longer-term work. Typically lives in Notion but use this in `docs/current-milestone.md`.

```
# Milestone Plan

## Metadata
- Project:
- Milestone:
- Owner:
- Target date:
- Status:
- Notion page:
- GitHub issue / project link:

## Objective

## Why this milestone matters

## Scope

## Non-goals

## Success criteria

## Dependencies

## Risks

## Open questions

## Inputs / linked docs
- `docs/project-spine.md`
- `docs/decision-log.md`
- linked Notion pages
- linked GitHub issues

## Planned outputs
- review artifact
- builder handoff
- implementation issues / PRs

## Latest summary
```

---

## Review Request

For critique and synthesis work. Use in `docs/reviews/active-review.md`.

```
# Review Request

## Metadata
- Project:
- Milestone:
- Reviewer type: ChatGPT / human / mixed
- Related Notion page:
- Related GitHub issue:

## What is being reviewed

## Context

## Proposal

## Tradeoffs

## Key assumptions

## Known risks

## Questions for review
1. What assumptions are weak?
2. What major risks are missing?
3. What is unnecessarily complex?
4. What should be decided now vs later?
5. What would make the builder handoff clearer?

## Source docs

## Desired write-back target
```

---

## Status Update

For tracking progress. Use in `docs/status-update.md` or Notion.

```
# Status Update

## Metadata
- Project:
- Milestone:
- Date:
- Owner:
- Notion page:
- GitHub issues / PRs:

## Current status

## What changed since last update

## Decisions made

## Blockers

## Risks

## Next steps

## Recommended write-backs
- Notion:
- Repo docs:
- GitHub:
```

---

## Session Summary

Quick wrap-up for any session. Not always durable but useful for handoffs.

```
# Session Summary

## Objective of session

## What was learned

## Decisions made or implied

## Open questions

## Recommended write-back target

## Suggested next step
```

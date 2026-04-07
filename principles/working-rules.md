# Working Rules — Tailored Stack

## Universal rules

1. Treat the repo project spine and decision log as more authoritative than chat history.
2. Treat Notion as the authoritative place for milestone status, ownership, blockers, and comments.
3. Treat GitHub issues and PRs as the authoritative place for code-linked execution.
4. Use OpenClaw for exploration, not durable memory.
5. Use ChatGPT for synthesis, review, and shaping outputs into durable artifacts.
6. Use Claude Code / Codex for implementation using the active handoff.
7. Prefer retrieval over large pasted context.
8. Avoid restating large documents unless asked.
9. Flag drift between Notion milestone plans, repo docs, and GitHub execution state.
10. End substantial sessions with a recommended write-back target.

## Context budget policy

Default sequence:

1. Read `docs/START_HERE.md`
2. Read `docs/project-spine.md`
3. Read one active task doc
4. Read at most 2 to 3 directly relevant references
5. Expand only if blocked or ambiguity remains

## Routing policy by task

### Exploration
Use OpenClaw first.
Read:
- `docs/project-spine.md`
- Notion milestone summary or `docs/current-milestone.md`

Output into:
- `docs/reviews/active-review.md`
- or `docs/handoffs/active-build.md`
- or Notion notes

### Review / critique
Use ChatGPT or humans.
Read:
- `docs/project-spine.md`
- `docs/current-milestone.md`
- `docs/reviews/active-review.md`
- only relevant source docs

Output into:
- `docs/reviews/active-review.md`
- `docs/current-milestone.md`
- Notion risks / decisions / comments

### Build
Use Claude Code or Codex.
Read:
- `docs/project-spine.md`
- `docs/handoffs/active-build.md`
- only referenced technical docs
- `docs/decision-log.md` if needed

Output into:
- code changes
- GitHub issue / PR updates
- `docs/decision-log.md`
- `docs/status-update.md`

### Tracking
Use Notion + GitHub.
Read:
- Notion milestone page
- GitHub issue / PR state
- `docs/status-update.md`

Output into:
- Notion milestone status
- `docs/status-update.md`
- issue / PR updates

## Document load policy

Each doc should ideally be classed as one of:

- `default`: commonly loaded first
- `role-specific`: loaded by certain modes only
- `reference`: load on demand
- `archive`: do not load by default

## Promotion rule

A chat or session output becomes durable only when it is written into one of:

- `docs/decision-log.md`
- `docs/status-update.md`
- `docs/current-milestone.md`
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- the relevant Notion milestone page
- the relevant GitHub issue or PR

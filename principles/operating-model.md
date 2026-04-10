# Operating Model — Tailored Stack

## Source of truth

- `docs/project-spine.md` and `docs/decision-log.md` are more authoritative than chat history.
- Notion is the authoritative place for milestone planning, ownership, status, blockers, and comments.
- GitHub is the authoritative place for code, technical docs, issues, pull requests, and code-linked execution.
- OpenClaw and chat threads are scratch space unless promoted into canonical docs.

## Information layers

### Stable project context
Examples:
- what the project is
- who it is for
- constraints
- success criteria
- key architecture assumptions

Primary docs:
- `docs/project-spine.md`
- `README.md`
- high-signal technical docs referenced from `docs/START_HERE.md`

### Milestone and planning context
Examples:
- milestone goal
- owner
- target date
- risks
- dependencies
- open questions

Primary location:
- Notion project page
- Notion milestone database
- `docs/current-milestone.md`

### Decision memory
Examples:
- selected approach
- deferred tradeoffs
- architecture choices
- product decisions that affect implementation

Primary doc:
- `docs/decision-log.md`

### Working implementation state
Examples:
- active handoff
- active review
- current tasks
- implementation blockers

Primary docs:
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- `docs/status-update.md`
- relevant GitHub issues / PRs

### Scratchpad and exploration
Examples:
- branching options
- rough plans
- raw prompts and transcripts
- speculative ideas

Primary location:
- OpenClaw sessions
- ChatGPT chats
- temporary notes

Only promote durable outputs from scratch space into canonical docs.

## Tool roles

### OpenClaw
Use for exploration and expansion.
It should produce:
- option sets
- structured summaries
- rough milestone plans
- candidate handoffs

### ChatGPT
Use for synthesis and review.
It should produce:
- clarified plans
- better structured artifacts
- tradeoff summaries
- review comments and simplifications

### Claude Code / Codex
Use for implementation work.
They should consume:
- the active handoff
- referenced technical docs
- the decision log when needed

### Notion
Use for milestone tracking and collaboration.
Keep status and comments here, not in long prompt histories.

### GitHub
Use for technical truth, durable implementation context, issues, and PRs.

## Context budget

Default sequence:

1. Read `docs/START_HERE.md`.
2. Read `docs/project-spine.md`.
3. Read one active task doc.
4. Read at most 2 to 3 directly relevant references.
5. Expand only if blocked or ambiguity remains.

Do not load archives or full history unless explicitly required.

## Routing by task

### Exploration
Use OpenClaw first.
Read:
- `docs/project-spine.md`
- the relevant Notion milestone summary or `docs/current-milestone.md`

Write back to:
- `docs/reviews/active-review.md`
- `docs/handoffs/active-build.md`
- or Notion notes

### Review and critique
Use ChatGPT or humans.
Read:
- `docs/project-spine.md`
- `docs/current-milestone.md`
- `docs/reviews/active-review.md`
- only relevant source docs

Write back to:
- `docs/reviews/active-review.md`
- `docs/current-milestone.md`
- or Notion risks, decisions, and comments

### Build
Use Claude Code or Codex.
Read:
- `docs/project-spine.md`
- `docs/handoffs/active-build.md`
- only referenced technical docs
- `docs/decision-log.md` if needed

Write back to:
- code changes
- GitHub issue / PR updates
- `docs/decision-log.md`
- `docs/status-update.md`

### Tracking
Use Notion and GitHub.
Read:
- the Notion milestone page
- GitHub issue / PR state
- `docs/status-update.md`

Write back to:
- Notion milestone status
- `docs/status-update.md`
- issue / PR updates

## Promotion rule

A session becomes durable only when it is written into one of:

- `docs/decision-log.md`
- `docs/status-update.md`
- `docs/current-milestone.md`
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- the relevant Notion milestone page
- the relevant GitHub issue or PR

Flag drift between Notion milestone plans, repo docs, and GitHub execution state.

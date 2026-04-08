# Context Model — Tailored Stack

## Source of truth by layer

- **Notion**: milestone planning, roadmap, owners, status, blockers, comments, collaboration
- **GitHub repo**: canonical technical truth, implementation-ready context, handoffs, decisions
- **GitHub issues / PRs**: execution state tied to code changes
- **OpenClaw / ChatGPT threads**: scratch space unless promoted

## Information layers

### 1. Stable project context
Examples:
- what the project is
- who it is for
- constraints
- success criteria
- key architecture assumptions

Primary docs:
- `docs/project-spine.md`
- `README.md`
- high-signal technical docs referenced from `START_HERE.md`

### 2. Milestone and planning context
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
- `docs/current-milestone.md` for repo-visible summary

### 3. Decision memory
Examples:
- selected approach
- deferred tradeoffs
- architecture choices
- product decisions that affect implementation

Primary doc:
- `docs/decision-log.md`

### 4. Working implementation state
Examples:
- active handoff
- active review
- current tasks
- implementation blockers

Primary docs:
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- GitHub issues / PRs
- `docs/status-update.md`

### 5. Scratchpad / exploration
Examples:
- branchy brainstorming
- competing options
- raw prompts and transcripts
- speculative business angles

Primary location:
- OpenClaw sessions
- ChatGPT chats
- temporary notes
- archive folders

Only promote durable outputs from scratchpad into canonical docs.

## Tool roles

### OpenClaw
Use for exploration and expansion only.
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
- comparison tables or tradeoff summaries
- review comments and simplifications

### Claude Code / Codex
Use for implementation work.
They should consume:
- active handoff
- referenced technical docs
- decision log when needed

### Notion
Use for milestone tracking and collaboration.
Keep status and comments here, not in long prompt histories.

### GitHub
Use for code, technical docs, issues, PRs, and durable implementation context.

## Retrieval rule

Load only the smallest sufficient context for the task:

1. orientation doc
2. active task doc
3. directly relevant supporting docs

Do not load archives or full history unless explicitly required.

## Write-back rule

Promote durable outcomes only:
- milestone updates to Notion
- decisions to `docs/decision-log.md`
- implementation handoffs to `docs/handoffs/active-build.md`
- review outputs to `docs/reviews/active-review.md`
- status summaries to `docs/status-update.md`
- code-linked execution updates to GitHub issues / PRs

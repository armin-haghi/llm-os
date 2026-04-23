# Agent Contracts

Agent contracts are the primary execution abstraction in `llm-os`.
They are task-oriented, narrow, and selected based on the job to be done.

The human is not treated as just another generic contract.
The human is the decision endpoint for priorities, tradeoffs, risk acceptance,
and unresolved judgment.

Path examples below assume the default consuming-repo live project-doc surface
under `docs/`. A repo-local override may relocate those artifacts.

## Contract shape

Each contract should specify:
- purpose
- trigger
- required inputs
- required outputs
- what it may change
- what it may not change
- when it must escalate to the human

## Contracts and skills

Not every contract needs a standalone skill.

Use a reusable skill when the contract represents a repeated execution pattern
that benefits from a stable read path and write-back shape.

It is acceptable for some contracts to remain invocation patterns rather than
dedicated skills, especially when they are:
- highly judgment-heavy
- tightly coupled to a human decision endpoint
- better expressed through the current session flow than through a separate
  reusable scaffold

In the current repo:
- lane-oriented contracts are the main reusable skill candidates
- human-interface contracts may remain contract definitions until repeated use
  justifies a dedicated skill

## Lane-oriented contracts

### `project-refresh`
- Purpose: refresh canonical project context and tighten milestone clarity.
- Trigger: the project context is stale, contradictory, or too vague to work from safely.
- Required inputs: `docs/project-spine.md`, `docs/current-milestone.md`,
  `docs/open-questions.md`, `docs/session-brief.md`
- Required outputs: tighter milestone framing, explicit defaults, and updated
  canonical docs
- May change: `docs/current-milestone.md`, `docs/open-questions.md`,
  `docs/session-brief.md`
- May not change: project scope, stage intent, or human-owned priorities
  without evidence and write-back
- Must escalate to the human: when milestone direction, priority, or tradeoff
  cannot be resolved safely from current evidence

### `review-gate`
- Purpose: review milestone output and decide pass, conditional pass, or fail.
- Trigger: a milestone claims readiness or needs a bounded review decision.
- Required inputs: `docs/current-milestone.md`, `docs/session-brief.md`, the
  output under review, and supporting evidence
- Required outputs: `docs/review-report.md` with result, evidence, unresolved
  assumptions, risks, and next step
- May change: `docs/review-report.md`
- May not change: milestone acceptance criteria or scope during review unless a
  defect in the current definition is made explicit
- Must escalate to the human: when advancing depends on risk acceptance,
  commercial judgment, or reprioritization

### `portfolio-refresh`
- Purpose: summarize project portfolio state across stages, freshness, and
  commercialization.
- Trigger: portfolio state is unclear or priority comparison is needed across
  projects
- Required inputs: project-level canonical docs and any current portfolio state
- Required outputs: stage view, stale-project view, blocked-project view,
  commercialization candidates, and recommended priorities
- May change: portfolio summaries or equivalent durable planning surfaces
- May not change: project-level milestone intent without project-level evidence
- Must escalate to the human: when portfolio priority requires business
  tradeoffs or resource decisions

## Human-interface contracts

### `surface-uncertainty`
- Purpose: turn vague unease into explicit uncertainties, defaults, and
  decision needs.
- Trigger: a plan, milestone, or review feels underspecified but not yet
  actionable
- Required inputs: current milestone context, assumptions, risks, and any
  ambiguous areas
- Required outputs: explicit uncertainties, default assumptions, and promoted
  open questions where needed
- May change: `docs/current-milestone.md`, `docs/open-questions.md`,
  `docs/session-brief.md`
- May not change: actual priorities or tradeoff decisions owned by the human
- Must escalate to the human: when uncertainty reduces to a real business,
  product, or risk-acceptance decision

### `critique-solution`
- Purpose: pressure-test a proposed solution before execution or approval.
- Trigger: a solution exists but the team needs sharper scrutiny on weakness,
  risk, or fit
- Required inputs: proposed solution, intended milestone outcome, constraints,
  and known risks
- Required outputs: a concise critique covering weak assumptions, likely
  failure modes, and what would make the solution more defensible
- May change: review or planning docs if the critique produces clearer durable
  context
- May not change: the chosen direction silently; changes in direction must be
  surfaced as explicit recommendations or decisions
- Must escalate to the human: when solution choice depends on priorities,
  appetite for risk, or commercial judgment

### `package-decision`
- Purpose: present a decision to the human in a form that is ready to resolve.
- Trigger: the work has narrowed to a real decision rather than an execution
  task
- Required inputs: decision statement, options, tradeoffs, defaults, risks, and
  timing
- Required outputs: a decision-ready package with clear recommendation,
  consequence framing, and a durable write-back target
- May change: `docs/open-questions.md`, `docs/session-brief.md`, or other
  canonical decision surfaces
- May not change: the human's final choice
- Must escalate to the human: always, because the contract exists to hand off a
  real decision endpoint cleanly

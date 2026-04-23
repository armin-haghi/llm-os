# llm-os change note — replace roles with agent contracts

This note captures a targeted change to apply on top of the current repo state.
It is not a full handoff rewrite.

## Why this change exists

The current model still thinks too much in broad classical roles.
That is not the right abstraction for this workflow.

The system should not be organized primarily around:
- Build agent
- Review agent
- Human

Instead, it should be organized around:
- stages for lifecycle
- lanes for recurring control functions
- task-oriented agent contracts for specific jobs
- the human as the decision endpoint for unresolved judgment

## What changes

### Replace broad role framing with agent-contract framing

Prefer:
- `core/agent-contracts.md`

instead of:
- `core/role-contracts.md`

The core operating model should stop assuming stable, broad “team member” roles as the main abstraction.

### Keep these unchanged

#### Stages
1. Opportunity framing
2. Solution shaping
3. Prototype
4. MVP build
5. Pilot / connected MVP
6. Operational hardening
7. Commercialization
8. Live iteration

#### Lanes
- review lane
- freshness lane
- commercial lane
- human decision lane

#### Serious session rule
1. load current context
2. do the intended work
3. reduce milestone uncertainty where possible
4. update canonical docs when clarity improves
5. escalate only residual human decisions

## New framing

Use this model:
- stages = where the project is in its lifecycle
- lanes = recurring operating functions that run across stages
- agent contracts = narrowly-scoped task executors
- human = decision endpoint for priorities, tradeoffs, risk acceptance, and unresolved judgment

## Initial agent contracts to define

Start small. The first useful contract set is:

### Lane-oriented
- `project-refresh`
- `review-gate`
- `portfolio-refresh`

### Human-interface
- `surface-uncertainty`
- `critique-solution`
- `package-decision`

These are task contracts, not job titles.

## What each agent contract should specify

For each contract define:
- purpose
- trigger
- required inputs
- required outputs
- what it may change
- what it may not change
- when it must escalate to the human

## Human treatment

Keep the human explicit in the system, but not as just another broad peer role.

The human should be treated as:
- the escalation point for unresolved judgment
- the owner of priorities and tradeoffs
- the accepter/rejecter of meaningful risk
- the final decision-maker when default assumptions are no longer safe

## File-level change to apply

### In `core/operating-model.md`
Replace role-centric language with:
- stages
- lanes
- stage / milestone / task / lane / agent-contract relationship
- the human as the decision endpoint

### Add or rename to `core/agent-contracts.md`
Document the task-oriented agent contracts.

### In assistant / session surfaces
Make sure they:
- do not lean on broad classical role language
- can invoke focused task agents
- still preserve milestone clarification and write-back rules

## Constraints

- Do not remove lanes.
- Do not remove the human from the model.
- Do not turn the human into just another generic role.
- Do not reintroduce broad classical org-chart thinking as the main abstraction.
- Do not rewrite the repo shell unless needed.
- Treat this as a delta change on top of current progress.

## Acceptance criteria

This change is complete when:
1. the repo no longer treats broad classical roles as the primary abstraction
2. `core/agent-contracts.md` exists or is clearly planned as the replacement for role contracts
3. stages and lanes remain unchanged
4. the human remains explicit as the decision endpoint
5. agent definitions are task-oriented and narrow
6. existing progress in the repo is preserved rather than replaced

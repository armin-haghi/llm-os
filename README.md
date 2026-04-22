# llm-os

`llm-os` is the reusable operating standard for agent-driven product work.
It keeps execution anchored to one active stage, one current milestone, and
durable write-back in canonical project docs instead of chat.

## Canonical files
- `core/operating-model.md`: roles, stages, lanes, and the serious session rule
- `core/role-contracts.md`: responsibilities and failure boundaries by role
- `core/change-policy.md`: how local patterns become operating standards
- `core/templates/minimal.md`: minimum shape for canonical project docs

## Canonical project docs
- `docs/project-spine.md`: stable project definition and success frame
- `docs/current-milestone.md`: active milestone, scope, and acceptance criteria
- `docs/open-questions.md`: unresolved decisions with owners and defaults
- `docs/session-brief.md`: fastest durable reload point for the next session
- `docs/review-report.md`: latest review outcome and required human decisions

## Core rule
A serious session should:
1. load current context
2. do the intended work
3. reduce milestone uncertainty where possible
4. update canonical docs when clarity improves
5. escalate only residual human decisions

# llm-os

`llm-os` is the reusable operating standard for agent-driven product work.
It keeps execution anchored to one active stage, one current milestone, and
durable write-back in canonical project docs instead of chat.

## Canonical files
- `core/operating-model.md`: stages, lanes, agent contracts, and the serious session rule
- `core/agent-contracts.md`: task-oriented contract definitions and human escalation boundaries
- `core/change-policy.md`: how local patterns become operating standards
- `core/external-skills.md`: boundary between core operating skills and capability-specific skills
- `core/freshness-model.md`: rules for detecting stale project context and deciding when refresh is needed
- `core/platform-playbook.md`: practical read-path, write-back, and escalation guidance across tools
- `templates/README.md`: template-layer overview

## Canonical templates
- `templates/project-spine.md`: stable project definition and success frame
- `templates/current-milestone.md`: active milestone, scope, and acceptance criteria
- `templates/open-questions.md`: unresolved decisions with owners and defaults
- `templates/session-brief.md`: fastest durable reload point for the next session
- `templates/review-report.md`: latest review outcome and required human decisions

## Expected project docs in a consuming repo
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

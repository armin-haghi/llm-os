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
- `core/decisions.md`: short record of load-bearing operating-model decisions
- `core/platform-playbook.md`: practical read-path, write-back, and escalation guidance across tools
- `templates/README.md`: template-layer overview

## Canonical templates
- `templates/AGENTS.md`: starter entrypoint for a consuming repo
- `templates/project-spine.md`: stable project definition and success frame
- `templates/current-milestone.md`: active milestone, scope, and acceptance criteria
- `templates/open-questions.md`: unresolved decisions with owners and defaults
- `templates/session-brief.md`: fastest durable reload point for the next session
- `templates/review-report.md`: latest review outcome and required human decisions
- `templates/project-overview.yaml`: minimum project overview input for cross-project status

## Initialize or Retrofit a Consuming Repo
Use the starter surfaces in this order:
1. audit the repo's current entry surfaces and project docs
2. create root `AGENTS.md` if missing
3. keep `docs/` as the default live project-doc surface, or declare a repo-local override in `AGENTS.md`
4. create only the missing canonical artifacts
5. create `project-overview.yaml`
6. fill the minimum working content before treating the repo as initialized

Use `skills/repo-initialize/SKILL.md` when you want the concrete initialization workflow.

## Expected project docs in a consuming repo
- `docs/project-spine.md`: stable project definition and success frame
- `docs/current-milestone.md`: active milestone, scope, and acceptance criteria
- `docs/open-questions.md`: unresolved decisions with owners and defaults
- `docs/session-brief.md`: fastest durable reload point for the next session
- `docs/review-report.md`: latest review outcome and required human decisions

`docs/` is the default live project-doc surface for consuming repos.

If a target repo uses a different live project-doc location, that override
should be declared in the target repo's local `AGENTS.md`, and local repo
instructions should override the llm-os default.

If a consuming repo's local instructions are missing or ambiguous, agents
should fall back to the canonical `llm-os` defaults rather than inventing repo
behavior ad hoc. In practice, that means consulting the canonical `llm-os`
`AGENTS.md`, `core/platform-playbook.md`, and only the directly relevant
`core/` guidance.

`llm-os` itself uses that override.
Its live project-doc surface lives under `llm-os-docs/project/` so `docs/`
stays reserved for the consuming-repo convention.

## This Repo's Live Project Docs
- `llm-os-docs/project/project-spine.md`: live project definition for this repo
- `llm-os-docs/project/current-milestone.md`: active milestone for this repo
- `llm-os-docs/project/open-questions.md`: unresolved project questions and decisions
- `llm-os-docs/project/session-brief.md`: fastest durable reload point for the next session in this repo
- `llm-os-docs/project/review-report.md`: latest review outcome for this repo

## Additional Repo Docs
- `llm-os-docs/doc-surface-decision.md`: explains the boundary between `core/`, `templates/`, default consuming-repo `docs/`, this repo's `llm-os-docs/project/`, and deeper explanatory docs
- `llm-os-docs/framework-comparison.md`: reference on what `llm-os` borrows from adjacent approaches and what it rejects
- `llm-os-docs/background/`: historical notes, assessments, and time-scoped design material

## Core rule
A serious session should:
1. load current context
2. do the intended work
3. reduce milestone uncertainty where possible
4. update canonical docs when clarity improves
5. escalate only residual human decisions

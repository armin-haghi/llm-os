# Operating Model

## Purpose
`llm-os` is the reusable operating standard for agent-driven product work.

## Canonical homes
- Notion: portfolio state, ownership, blockers, priorities, human decisions
- Project repo: code and project-specific durable context
- llm-os: reusable operating model, skills, templates
- Entry points: interfaces only, not source of truth

## Roles
- Build agent
- Review agent
- Human

## Stages
1. Opportunity framing
2. Solution shaping
3. Prototype
4. MVP build
5. Pilot / connected MVP
6. Operational hardening
7. Commercialization
8. Live iteration

## Lanes
- Review lane
- Freshness lane
- Commercial lane
- Human decision lane

## Working units
- Stage: lifecycle context
- Milestone: bounded outcome within a stage
- Task: concrete execution step
- Lane: recurring cross-stage operating function

Rules:
- a project has one active stage
- a milestone belongs to one primary stage
- tasks move the active milestone forward
- lanes can operate inside any stage or milestone

## Serious session rule
A serious session should:
1. load current context
2. do the intended work
3. reduce milestone uncertainty where possible
4. update canonical docs when clarity improves
5. escalate only residual human decisions

## Write-back expectation
A serious session is not complete until durable changes are written back to canonical project docs.

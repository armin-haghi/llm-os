# Operating Model

## Purpose
`llm-os` is the reusable operating standard for agent-driven product work.
It keeps project execution grounded in a clear stage, a bounded milestone, and
durable project memory.

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
- Stage: lifecycle context for the project right now
- Milestone: bounded outcome within a stage
- Task: concrete execution step that advances the milestone
- Lane: recurring cross-stage operating function

Rules:
- a project has one active stage at a time
- a milestone belongs to one primary stage
- tasks should advance acceptance criteria or reduce blocking uncertainty
- lanes can operate inside any stage or milestone without becoming the stage

## Serious session rule
A serious session should:
1. load current context
2. do the intended work
3. reduce milestone uncertainty where possible
4. update canonical docs when clarity improves
5. escalate only residual human decisions

## Write-back expectation
A serious session is not complete until durable changes are written back to
canonical project docs when clarity or outcomes improve.

## Reference influences

This operating model is informed by several adjacent approaches, but does not fully adopt any one of them.

- **Specialist agent / role-based systems**  
  Influence on explicit roles and mode selection.  
  In this repo, that shows up as `Build agent`, `Review agent`, and `Human`.

- **Shaping-first product methods**  
  Influence on bounded milestones, scope discipline, and reducing ambiguity before execution.  
  In this repo, that shows up as the distinction between `stage`, `milestone`, and `task`.

- **Working-backwards / customer-value framing**  
  Influence on clarifying user value and commercial logic before build.  
  In this repo, that shows up most strongly in `Opportunity framing`, `Solution shaping`, and the `Commercial lane`.

- **Handbook-first / operating-system-style documentation**  
  Influence on durable written context, explicit operating rules, and treating chat as scratch space unless promoted.  
  In this repo, that shows up in canonical docs, write-back expectations, and change policy.

## Non-goals

This operating model is not:
- a generic company operating system
- a full agile methodology
- a backlog-heavy task management framework
- a coding-only assistant setup
- a chat transcript archive

It is a lightweight operating standard for agent-driven product work with durable context, bounded milestones, and explicit human decision routing.
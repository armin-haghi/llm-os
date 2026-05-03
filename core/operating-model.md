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

## Agent contracts
- Agent contracts are narrowly-scoped task executors.
- A contract is selected because the task matches it, not because a stable
  team-member role exists.
- The human remains explicit as the decision endpoint for unresolved judgment.

## Stages

Stages describe the project's current lifecycle context.
They should be assigned based on the dominant uncertainty, not the amount of
code that exists.

A project can have a repo, a deployed preview, real data, or working automation
and still be in `Prototype` if the main uncertainty is whether the product shape
works.

Ordered stages:

1. `Opportunity framing`
   - Main question: is this a real opportunity worth pursuing?
   - Use when problem, user, value, urgency, or strategic reason are still
     unclear.
2. `Solution shaping`
   - Main question: what should the first useful solution be?
   - Use when the opportunity seems worth exploring but product shape, scope,
     or wedge is still being chosen.
3. `Prototype`
   - Main question: does this product shape work?
   - Use when building or testing proof through code, demos, data, workflows,
     or early deployments, while core product shape is still being learned.
4. `MVP build`
   - Main question: can we build the agreed first usable product?
   - Use only when the target user/workflow is clear, first product scope is
     chosen, and the main work is execution rather than discovery.
5. `Pilot / connected MVP`
   - Main question: can a real or near-real workflow use this?
   - Use when the product is connected to actual users, data, integrations, or
     operational workflows and feedback from use matters.
6. `Operational hardening`
   - Main question: can this run reliably?
   - Use when the product basically works and the focus is reliability,
     observability, security, deployment, maintainability, or support.
7. `Commercialization`
   - Main question: can this be packaged, sold, distributed, or positioned?
   - Use when the main work is pricing, packaging, go-to-market, sales,
     distribution, or commercial proof.
8. `Live iteration`
   - Main question: how should this improve based on live use?
   - Use when the product is already live and the main loop is ongoing
     improvement.

Stage assignment rules:

- Pick the stage by dominant uncertainty, not implementation progress.
- When unsure between `Prototype` and `MVP build`, prefer `Prototype`.
- Do not use `MVP build` merely because code exists or a preview is deployed.
- Use `MVP build` only when the first usable product scope is chosen and the
  target user/workflow is clear.
- A project has one active stage at a time.
- A milestone belongs to one primary stage.

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
- Agent contract: task-oriented execution boundary with explicit inputs,
  outputs, and escalation conditions

Rules:
- a project has one active stage at a time
- a milestone belongs to one primary stage
- tasks should advance acceptance criteria or reduce blocking uncertainty
- lanes can operate inside any stage or milestone without becoming the stage
- agent contracts should stay narrow and task-specific
- the human is the decision endpoint when default assumptions stop being safe

Relationship summary:
- stage = lifecycle location
- milestone = bounded outcome inside the active stage
- task = concrete move that advances the milestone
- lane = recurring control function that can operate across stages
- agent contract = the narrowly-scoped executor used for a specific task
- human = the decision endpoint when execution reaches unresolved judgment

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
  Influence on explicit execution boundaries and mode selection.
  In this repo, that shows up as narrow `agent contracts` plus explicit human escalation.

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

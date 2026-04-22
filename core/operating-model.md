# LLM-OS Minimal Core — Operating Model

This file is canonical.

## Source of truth order
1. `core/operating-model.md`
2. `core/role-contracts.md`
3. `core/change-policy.md`
4. `core/templates/minimal.md`
5. Project-local durable docs (for example `docs/project-spine.md`, `docs/current-milestone.md`, `docs/decision-log.md`)

If guidance conflicts, follow the highest item in this list.

## System boundaries
- **Notion**: milestone planning, ownership, status, blockers, and collaboration.
- **GitHub**: code, technical docs, issues, pull requests, and execution history.
- **Repo docs**: durable implementation-ready context.
- **Chat sessions**: scratch space unless promoted per the change policy.

## Default context budget
Read the smallest sufficient context:
1. project entry doc (`docs/START_HERE.md` when present)
2. stable context (`docs/project-spine.md`)
3. one active doc (`docs/current-milestone.md` or `docs/handoffs/active-build.md` or `docs/reviews/active-review.md`)
4. only directly relevant references

Do not load archives or broad history unless blocked.

## Routing by intent
- **Explore**: generate options and risks; output a review artifact.
- **Plan**: shape milestone scope and acceptance criteria.
- **Build**: execute against an active handoff and repo truth.
- **Track**: update status and decisions in durable systems.

## Non-goal
This model does not treat long chat transcripts as durable project memory.

# LLM-OS Canonical Core — Operating Model

This file is canonical.

## Source of truth order
1. `core/operating-model.md`
2. `core/role-contracts.md`
3. `core/change-policy.md`
4. `core/templates/minimal.md`
5. Legacy docs (compatibility only; never default policy)

If guidance conflicts, follow the highest item.

## Core units
- **Stage**: lifecycle phase of work.
- **Milestone**: the current outcome being driven to completion.
- **Task**: smallest executable unit that advances a milestone.
- **Lane**: ownership channel for tasks within a stage.

## Canonical stages
1. **Scope** — define milestone intent and constraints.
2. **Plan** — choose approach, sequence tasks, define acceptance.
3. **Build** — execute implementation tasks.
4. **Review** — validate outputs, risks, and fit.
5. **Ship / Track** — capture decisions, status, and next milestone.

## Canonical lanes
- **Human lane**: product intent, priority, approvals, tradeoff calls.
- **Build agent lane**: implementation planning and execution tasks.
- **Review agent lane**: critique, risk checks, and quality validation.

## Relationship: stage -> milestone -> task -> lane
- A project can have many milestones, but only one **active milestone** by default.
- Each milestone progresses through stages in order (with allowed loopbacks from Review to Plan/Build).
- Each stage contains a task list.
- Every task is assigned to exactly one lane: Human, Build agent, or Review agent.
- Progress is tracked at milestone level; task state is the operational detail.

## Default artifact surface (canonical)
Use `docs/current-milestone.md` as the default working surface for planning, execution, and tracking.
Other artifacts are optional and should be introduced only when needed.

## Context budget
Read the smallest sufficient context:
1. `docs/current-milestone.md`
2. only directly referenced supporting docs
3. legacy docs only when migrating or resolving ambiguity

## Non-goals
- No transcript-as-memory behavior.
- No parallel operating models across legacy documents.

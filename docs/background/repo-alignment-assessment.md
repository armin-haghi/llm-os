# Repo Alignment Assessment

Date: 2026-04-24

This note captures a repo-level assessment of how well `llm-os` is aligned on
what it is trying to achieve today, including a check of the planned next
slices. It is a background assessment, not a canonical operating-model file.

## Overall assessment

`llm-os` is conceptually aligned.

The core thesis is clear and consistent:
- stages define lifecycle position
- milestones bound the current outcome
- lanes provide recurring control functions
- agent contracts are narrow task executors
- the human is the decision endpoint
- durable docs matter more than chat history

That model is expressed cleanly in:
- `core/operating-model.md`
- `core/agent-contracts.md`
- `core/templates/minimal.md`
- `core/change-policy.md`

The repo is less aligned at the entry-surface and workflow level.

The current state looks like a strong minimal core plus partially completed
integration work around read paths, modes, entrypoints, and supporting skills.
The next slices mostly reinforce the current direction rather than changing it.

## What is working

### The abstraction stack is coherent

The repo has a defensible core vocabulary:
- stage
- milestone
- task
- lane
- agent contract
- human decision endpoint

This is a meaningful improvement over broader role-based agent framing.

### The repo is staying lightweight

The core files are short, readable, and opinionated without becoming a full
process framework. That matches the stated non-goals and keeps the system
usable across tools and projects.

### The next slices mostly fit the current direction

The planned additions in `docs/background/next-slices.md` mostly read as
missing glue:
- routing discipline
- platform playbook
- human-input and topic-surfacing support
- external-skills boundary
- freshness and decisions handling

These do not fight the current model. They mostly fill in incomplete operating
surfaces.

## Gaps and inconsistencies

### 1. No single stable read path yet

Different files describe different default loading behavior.

- `AGENTS.md` says serious project work should start with
  `docs/session-brief.md` and `docs/current-milestone.md`.
- `skills/llm-os-session/SKILL.md` starts with `docs/project-spine.md`.
- `docs/background/ops-model-delta.md` proposes a stricter sequence of
  `AGENTS.md -> active milestone -> current task / plan -> decisions`.

This is the biggest live inconsistency in the repo because minimal context is
one of the main promises of the system.

### 2. Mode model is only partially normalized

`AGENTS.md` defines:
- `new-project`
- `existing-project`
- `ongoing-session`
- `operating-model-update`

But `docs/background/ops-model-delta.md` also talks about `execution` and
`review` as if they were modes, without cleanly mapping them to the current
entry surface. The routing idea is good, but it has not been fully integrated
into the live mode model.

### 3. Entry-surface work is unfinished

The repo says entry points are interfaces rather than source of truth, which is
the right design.

But the intended surface is incomplete:
- `AGENTS.md` exists
- `README.md` exists
- `skills/llm-os-session/SKILL.md` exists
- `ASSISTANT.md` is still missing

That leaves the multi-entrypoint story incomplete, especially since the
background notes still assume `ASSISTANT.md` is part of the operating surface.

### 4. Background/reference boundaries are conceptually right but structurally loose

The repo clearly wants background material to be non-default context.

That rule is stated well, but the structure is not fully settled:
- several notes refer to `/background`
- the live repo stores them under `docs/background/`
- one planned slice still points to `/background/frameworks/...`

This is a small issue, but it weakens a load-bearing distinction: what is
canonical execution context vs. what is optional reference material.

### 5. Contract definitions are ahead of executable skills

`core/agent-contracts.md` defines both:
- lane-oriented contracts
- human-interface contracts

The implemented skills currently cover the lane side more than the human-side
interaction layer:
- `project-refresh`
- `review-gate`
- `portfolio-refresh`

The human-interface side is still mostly planned:
- `surface-uncertainty`
- `critique-solution`
- `package-decision`
- `capture-human-input` and `surface-human-topics` in next slices

This means the conceptual model currently describes more behavior than the repo
can directly invoke.

### 6. The repo is still more template than self-hosted operating system

The canonical project docs are present, but they are still mostly template
forms rather than a live instantiated example of `llm-os` running on itself:
- `docs/project-spine.md`
- `docs/current-milestone.md`
- `docs/open-questions.md`
- `docs/session-brief.md`
- `docs/review-report.md`

That is acceptable for a scaffold, but it is still a proof gap if the goal is
to show that the operating loop works end-to-end on the repo itself.

## How the next slices change the picture

The next slices suggest the repo is not confused about direction.
It is mostly unfinished in a few key integration areas.

The most important near-term slices are the ones that reduce ambiguity in the
live surface:
1. enforce one read path
2. normalize routing vs. modes
3. finish the entry-surface set
4. define the platform playbook
5. make the human-interface contracts real

By contrast, later additions like schemas, execution flags, and broader stage
skills should probably wait until the current operating surface is internally
consistent.

## Recommended interpretation

The repo is aligned on what it is trying to become, but not yet fully aligned
in how that intent is expressed across all files.

Put differently:
- the core model is strong
- the supporting surfaces still drift
- the next slices mostly identify the correct missing pieces

The highest-value work now is not inventing more theory.
It is collapsing the repo to one coherent operating surface around the current
core.

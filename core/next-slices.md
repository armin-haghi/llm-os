# Next slices

This file tracks the next meaningful additions to `llm-os`.
It is not a full backlog. It exists to keep future slices visible without turning
the operating model into a second project-management system.

## How to use this file

For each item, keep only:
- status
- why it matters
- trigger to do it
- notes

Status values:
- `now`
- `next`
- `later`
- `blocked`
- `deferred`

A slice should move into active work only when its trigger is true.

---

## Now

### 1. Replace broad roles with agent contracts
- Status: `now`
- Why it matters: broad classical roles are not the right abstraction for this workflow. The system should use narrowly-scoped task agents and keep the human explicit as the decision endpoint.
- Trigger to do it: before the next core cleanup pass
- Notes:
  - replace `core/role-contracts.md` with `core/agent-contracts.md`
  - keep stages and lanes unchanged
  - keep the human explicit as the decision endpoint

### 2. Cheap OpenClaw input skill
- Status: `now`
- Why it matters: there needs to be a lightweight way to capture my thoughts conversationally, using a cheaper model by default, without forcing a full build/review context.
- Trigger to do it: before relying on OpenClaw as the human-facing control surface
- Notes:
  - likely name: `capture-human-input`
  - default output should update the right durable artifact
  - escalate to a stronger model only when explicitly triggered or clearly needed

### 3. Human-topic surfacing skill
- Status: `now`
- Why it matters: the system should proactively surface decision-worthy, uncertainty-heavy, and review-worthy issues to the human by project.
- Trigger to do it: before using llm-os as a real operating loop across multiple active projects
- Notes:
  - likely name: `surface-human-topics`
  - should package:
    - project
    - stage
    - milestone
    - recommendation
    - uncertainty
    - risks
    - explicit human question
    - default next step if approved

### 4. Platform playbook
- Status: `now`
- Why it matters: the model needs one practical guide for how to use OpenClaw, Codex, Claude Code, and other entry points without bloating README.
- Trigger to do it: before onboarding the first real project into this system
- Notes:
  - create `core/platform-playbook.md`
  - include:
    - when to use each platform
    - what file to read first
    - what each should write back
    - when to escalate to human

### 5. Minimum project overview input format
- Status: `now`
- Why it matters: `portfolio-refresh` exists conceptually, but there must be a minimum shape for project-overview input before it can work reliably.
- Trigger to do it: before trying to run project-overview refreshes for real
- Notes:
  - minimum fields:
    - project
    - stage
    - active milestone
    - freshness
    - blocker
    - next action
    - commercial signal

---

## Next

### 6. Notion control-tower schema and views
- Status: `next`
- Why it matters: project visibility across multiple active efforts needs a durable control surface.
- Trigger to do it: when 2–3 active projects need cross-project prioritization
- Notes:
  - define project database fields
  - define views for:
    - by stage
    - stale
    - blocked
    - commercialization candidates
    - needs human decision

### 7. Concurrency rules
- Status: `next`
- Why it matters: a project may have concurrent work, but the model needs a rule for when parallel work is safe.
- Trigger to do it: when one project starts having multiple parallel workstreams
- Notes:
  - a project should still have one active stage
  - a project should still have one primary active milestone
  - concurrent work is allowed only if threads advance the same milestone or clearly bounded sub-slices of it

### 8. External skills boundary
- Status: `next`
- Why it matters: the system needs a rule for whether a capability belongs in llm-os core or in a separate skill store.
- Trigger to do it: before adding the first non-core external capability
- Notes:
  - likely create `core/external-skills.md`
  - rule of thumb:
    - core skill = improves the operating model across projects
    - external skill = solves a specific capability problem
  - example:
    - `surface-human-topics` belongs in llm-os core
    - something like Graphify belongs outside core

### 9. Freshness model
- Status: `next`
- Why it matters: stale docs are one of the main failure modes for this system.
- Trigger to do it: when real project docs start drifting in practice
- Notes:
  - create `core/freshness-model.md`
  - define:
    - what stale means
    - what must be refreshed automatically
    - what can remain unchanged

### 10. Decisions doc
- Status: `next`
- Why it matters: major operating-model decisions should be durable and discoverable.
- Trigger to do it: when the core starts evolving beyond small edits
- Notes:
  - create `core/decisions.md`
  - keep it short
  - record only load-bearing operating decisions

---

## Later

### 11. Stage skills expansion
- Status: `later`
- Why it matters: stages should eventually become executable through dedicated task agents, not just conceptual phases.
- Trigger to do it: when the same stage work is repeated manually across multiple projects
- Notes:
  - initial candidate set:
    - `opportunity-frame`
    - `solution-shape`
    - `prototype`
    - `mvp-build`
    - `pilot-connect`
    - `operational-harden`
    - `commercialize`
    - `live-iterate`

### 12. Schemas
- Status: `later`
- Why it matters: schemas matter once multiple tools or automations need to read and write the same artifacts reliably.
- Trigger to do it: when llm-os starts depending on automation or machine-readable interchange
- Notes:
  - likely schemas:
    - `project-status.yaml`
    - `review-report.yaml`
    - `session-brief.yaml`

### 13. Human-scope workflow design
- Status: `later`
- Why it matters: the model already points toward dedicated human-facing flows, but they need a clean formalization.
- Trigger to do it: when OpenClaw becomes the real decision/uncertainty/review interface
- Notes:
  - conversational input
  - decision packaging
  - uncertainty surfacing
  - critical review
  - optional deeper research

### 14. Engineering baseline
- Status: `later`
- Why it matters: the operating model needs just enough engineering discipline to avoid chaos, but not a heavy engineering manifesto.
- Trigger to do it: when the first real project reaches operational hardening
- Notes:
  - probably a small `core/engineering-baseline.md`
  - should cover only:
    - observable acceptance criteria
    - evidence-based review
    - testing expectations by milestone
    - hardening expectations around environments, secrets, observability

---

## Current design direction

The operating model should continue moving toward:

- stages as lifecycle structure
- lanes as recurring control functions
- task-oriented agent contracts instead of broad classical roles
- the human as the decision endpoint for unresolved judgment
- canonical project docs as durable memory
- serious sessions that improve milestone clarity while they work
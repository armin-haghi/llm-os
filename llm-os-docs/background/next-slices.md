# Next slices

This file tracks the next meaningful additions to `llm-os`.

Historical note: file paths or assumptions inside this note may reflect older
repo structure when a slice was first proposed.
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
- no new `now` items currently
- the first-cut operating surface is materially in place
- use the active milestone docs for the current cleanup and validation pass

---

## Operating Model Delta

### Add lightweight guardrails
- status: now
- why it matters: prevents scope creep and overengineering
- trigger to do it: multi-file changes or unclear requirements
- notes: smallest viable change; no unrelated edits; escalate to Plan when unclear

---

## Next

### Notion control-tower schema and views
- status: next
- why it matters: provides cross-project visibility and prioritization
- trigger to do it: 2–3 active projects require coordination
- notes: define project fields and views (stage, stale, blocked, commercialization, human decision)

---

### Concurrency rules
- status: next
- why it matters: ensures parallel work does not fragment execution
- trigger to do it: multiple concurrent workstreams in one project
- notes: one active stage, one primary milestone; parallel work only within same milestone

---

### Borrow adaptive planning from BMAD
- status: next
- why it matters: aligns planning depth with task complexity
- trigger to do it: tasks exceed single-session scope or involve dependencies
- notes: scale planning depth only; do not introduce roles or workflows

---

### Borrow execution verbs from gstack
- status: next
- why it matters: improves clarity in execution and quality control
- trigger to do it: repeated need for explicit review/qa/ship steps
- notes: map to lifecycle (Review/Ship/Reflect); no command system

---

### Model right-sizing with safe escalation
- status: next
- why it matters: routes each task to the smallest adequate model by default, keeping cost and latency low while ensuring high-complexity work gets appropriate capability
- trigger to do it: after first real project onboarding to validate where the boundaries actually are
- notes: smaller models handle capture, formatting, summarization, classification, simple transformations; must escalate (not guess) when exceeding capability; escalation triggers: unclear instructions, missing context, low confidence, high-risk changes, need for synthesis/planning/judgment; stronger models handle planning, synthesis, architecture, critical review, final decisions

---

## Later

### Stage skills expansion
- status: later
- why it matters: turns stages into executable capabilities
- trigger to do it: repeated manual stage work across projects
- notes: opportunity-frame, solution-shape, prototype, mvp-build, pilot-connect, operational-harden, commercialize, live-iterate; early-stage external candidates may exist first and should only be promoted after reuse proves they reduce confusion

---

### Schemas
- status: later
- why it matters: enables reliable multi-tool interaction
- trigger to do it: need for machine-readable artifacts
- notes: project-status.yaml, review-report.yaml, session-brief.yaml

---

### Human interaction workflow design

- status: next
- why it matters: formalizes how human input, decisions, uncertainty, and review move through the system across all entry points
- trigger to do it: human-facing workflows start happening across multiple tools or contexts
- notes: support OpenClaw, Codex, Claude, Notion, and direct repo edits; define input capture, decision packaging, uncertainty surfacing, review requests, and write-back rules

---

### Engineering baseline
- status: later
- why it matters: adds minimal discipline for production readiness
- trigger to do it: first project reaches operational hardening
- notes: acceptance criteria, evidence-based review, testing expectations, environments, observability

---

### Add execution flags (`[careful]`, `[freeze]`)
- status: later
- why it matters: provides lightweight control for risky or scope-sensitive work
- trigger to do it: large diffs or repeated scope drift
- notes: optional annotations only

---

### Add tool compatibility outputs
- status: later
- why it matters: ensures consistent behavior across tools
- trigger to do it: workflows span multiple tools regularly
- notes: generate CLAUDE.md, Codex instructions, skills from AGENTS.md only

---

## Current design direction

The operating model should continue moving toward:

- stages as lifecycle structure
- lanes as recurring control functions
- task-oriented agent contracts instead of broad roles
- the human as the decision endpoint
- canonical project docs as durable memory
- sessions that improve milestone clarity while executing

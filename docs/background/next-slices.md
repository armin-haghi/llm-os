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

### Replace broad roles with agent contracts
- status: now
- why it matters: broad roles are the wrong abstraction; the system should use narrowly scoped task agents with the human as decision endpoint
- trigger to do it: before next core cleanup pass
- notes: replace `core/role-contracts.md` with `core/agent-contracts.md`; keep stages and lanes unchanged

---

### Cheap OpenClaw input skill
- status: now
- why it matters: enables lightweight conversational input without pulling full execution context
- trigger to do it: before using OpenClaw as primary control surface
- notes: `capture-human-input`; writes to correct durable artifact; escalates model only when needed

---

### Human-topic surfacing skill
- status: now
- why it matters: ensures decision-worthy and uncertain items are surfaced to the human
- trigger to do it: before running multiple active projects in parallel
- notes: `surface-human-topics`; include project, stage, milestone, recommendation, uncertainty, risks, explicit question, default next step

---

### Platform playbook
- status: now
- why it matters: provides a single practical guide across tools without bloating README
- trigger to do it: before onboarding first real project
- notes: `core/platform-playbook.md`; define tool usage, read order, write-back expectations, escalation points

---

### Minimum project overview input format
- status: now
- why it matters: enables reliable project overview refresh
- trigger to do it: before running portfolio refresh in practice
- notes: fields = project, stage, active milestone, freshness, blocker, next action, commercial signal

---

## Operating Model Delta

### Add routing layer
- status: now
- why it matters: introduces consistent execution flow without adding agents
- trigger to do it: ambiguity inside a mode or AGENTS.md update
- notes: `Think → Plan → Build → Review → Ship → Reflect`; implicit within modes

---

### Add `operating-model-update` mode
- status: now
- why it matters: isolates changes to the operating model from execution work
- trigger to do it: any change to AGENTS.md, ASSISTANT.md, templates, or workflow rules
- notes: require reason, impact, affected files; follow with consistency check

---

### Enforce default read path
- status: now
- why it matters: keeps context minimal and predictable
- trigger to do it: agent attempts to load broader context
- notes: only AGENTS.md → milestone → task/plan → decisions; exclude `/background` unless explicitly referenced

---

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

### External skills boundary
- status: next
- why it matters: prevents core from absorbing capability-specific logic
- trigger to do it: before adding first non-core capability
- notes: `core/external-skills.md`; core = operating model improvement, external = capability-specific

---

### Freshness model
- status: next
- why it matters: prevents drift in project artifacts
- trigger to do it: docs begin to diverge from reality
- notes: define stale criteria and refresh rules

---

### Decisions doc
- status: next
- why it matters: keeps load-bearing decisions durable and discoverable
- trigger to do it: operating model evolves beyond small edits
- notes: `core/decisions.md`; keep short and focused

---

### Add background framework docs
- status: next
- why it matters: enables structured borrowing without polluting execution context
- trigger to do it: need to reference external frameworks
- notes: `/background/frameworks/{bmad.md, gstack.md, comparison.md}`

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

## Later

### Stage skills expansion
- status: later
- why it matters: turns stages into executable capabilities
- trigger to do it: repeated manual stage work across projects
- notes: opportunity-frame, solution-shape, prototype, mvp-build, pilot-connect, operational-harden, commercialize, live-iterate

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
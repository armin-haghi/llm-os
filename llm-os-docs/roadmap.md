# LLM-OS Roadmap

This roadmap is the canonical view of how `llm-os` should evolve.

It is intentionally higher level than `llm-os-docs/project/current-milestone.md`.
The current milestone owns active execution detail. This roadmap owns direction,
sequencing, design references, and decision points.

## Source-of-truth rule

- This file is the canonical roadmap for `llm-os` as an operating standard.
- `llm-os-docs/project/current-milestone.md` is the canonical active milestone.
- `llm-os-docs/version-log.md` is the canonical compatibility history.
- Notion should mirror only the current status, next action, next decision, and
  links back to these repo files.

## Product thesis

`llm-os` is a lightweight control plane for AI-assisted product development.

It should let a human run multiple product streams across ChatGPT, Claude,
Codex, OpenClaw, local models, Notion, and GitHub without losing product intent,
current state, human decisions, agent handoffs, or repo write-backs.

It should coordinate agents and tools. It should not try to replace them.

## Design references and intentional differences

LLM-OS learns from adjacent agent and development frameworks, but does not try to
become any one of them.

| Reference pattern | What it teaches | What LLM-OS should borrow | What LLM-OS should avoid |
| --- | --- | --- | --- |
| Spec-driven development / GitHub Spec Kit | Implementation should preserve durable intent, not disposable planning text. | Treat milestones, project spine, and run handoffs as intent anchors before build work starts. | Do not become only a spec generator. LLM-OS also owns portfolio state, write-back discipline, and source-of-truth alignment. |
| BMAD-style agentic agile workflows | Structured stages, reusable artifacts, and just-in-time context help agents work more reliably. | Borrow stage-aware workflows and scale-adaptive depth. | Avoid too many personas, heavy ceremony, and a large default read path. |
| LangGraph-style durable execution | Long-running agent work needs state, pause/resume, interrupts, human checkpoints, and auditability. | Keep run states, blocked/waiting-human/done semantics, and resumable handoffs in lightweight form. | Do not build a full orchestration runtime before the manual control-plane loop is proven. |
| CrewAI-style flows and crews | Workflow control and autonomous delegation are different concerns. | Keep orchestration separate from bounded agent runs. | Do not make every task a multi-agent crew. Most work should be one bounded run plus review/write-back. |
| OpenAI / Anthropic coding-agent direction | Native coding agents, skills, repo context, connectors, memory, and parallel execution will keep improving. | Coordinate Codex, Claude Code, OpenClaw, and other tools through shared state and handoff rules. | Do not duplicate coding agents or build a competing coding framework. |

## Roadmap summary

| Milestone | Status | Goal | Notes |
| --- | --- | --- | --- |
| M0 — Explain the intent | Done | Make clear what LLM-OS is for and why it exists. | README and overview now explain the human-facing purpose. |
| M1 — Repo-backed operating surface | Done | Establish `AGENTS.md`, project docs, templates, session brief, milestone, and review report. | Corresponds to compatibility version `0.1`. |
| M2 — Control Tower and Agent Run Queue | Done / needs use | Add Notion portfolio state and bounded run dispatch while keeping repo docs canonical. | Corresponds to version `0.2`. Needs validation on real projects. |
| M3 — Consistency and compatibility tracking | Built / needs use | Detect repo/Notion/run-handoff drift and track which repos need LLM-OS migration. | Corresponds to version `0.3`. |
| M4 — Repo state, review tracking, and write-back closeout | Built / needs use | Track branch/commit, review need, Notion write-back status, follow-up run need, and minute timestamps. | Corresponds to versions `0.4` and `0.5`. |
| M5 — Orchestration validation across active projects | Active | Test the control tower, run queue, consistency checks, and write-back closeout on real active projects. | Current active milestone. Do not expand the framework heavily before this is validated. |
| M6 — Parallel stream model | Decision pending | Decide whether parallel streams need a first-class object or can remain milestones plus bounded runs. | Should be decided from observed project-sweep and selected-project use. |
| M7 — Model routing and cost-aware agents | Not started | Define what cheap/local models can do, when to escalate, and when to use coding agents. | Should remain simple and policy-driven. |
| M8 — Stage skills | Not started | Add skills for opportunity framing, solution shaping, prototype, MVP, pilot, hardening, commercialization, and iteration. | Add only after the orchestration loop proves useful. |
| M9 — Automation and concurrency | Deferred | Add locking, parallel agent coordination, branch/worktree conventions, and stronger run automation. | Do not build before manual orchestration semantics are clear. |

## Active milestone

The active milestone is recorded in `llm-os-docs/project/current-milestone.md`.

Current goal:

> Test and harden the minimal control-tower, Agent Run Queue, and shared
> orchestration path across active projects.

This means the next real work should run LLM-OS against live projects and verify
that the system can:

- refresh project state without relying on chat memory
- detect stale Notion/repo state
- identify LLM-OS compatibility gaps
- create or select one bounded agent run
- execute or dispatch the run from a declared read path
- close the run with repo and Notion write-back status recorded
- surface the next human decision clearly

## Decision points

### D1 — Is the current control-tower shape enough?

Question: after running project sweep on `llm-os`, Costmind, and one more active
project, are Project Control Tower plus Agent Run Queue sufficient?

Possible outcomes:

- keep the current shape and only tune fields/views
- add a lightweight project-stream object
- simplify the queue if it starts acting like a backlog

### D2 — Do parallel streams need to be first-class?

Question: should streams such as product spec, backend build, evaluation,
design, launch, and hardening be represented explicitly?

Default until proven otherwise:

- keep streams implicit in milestones and bounded runs
- add a first-class stream object only if real project work shows confusion,
  collisions, or hidden dependencies

### D3 — How much model routing is enough?

Question: can model routing stay as a simple escalation policy, or does it need
schema support?

Default:

- cheap/local models handle intake, summarization, formatting, and first-pass
  organization
- stronger models handle product tradeoffs, architecture, synthesis, critique,
  and high-ambiguity decisions
- coding agents handle implementation and tests
- escalation should be suggested when confidence, context, risk, or complexity
  exceeds the current agent's capability

### D4 — When should automation begin?

Question: when should LLM-OS move from human-readable orchestration to automated
workflow execution?

Default:

- automate only after manual semantics are stable
- prefer clear state and write-back rules before locks, runners, or background
  agents

## Near-term roadmap

### Next: Project sweep validation

Run a project sweep against:

- `llm-os`
- Costmind
- one more active repo-backed project

Expected output:

- project status table
- stale-state findings
- compatibility gaps
- waiting-human decisions
- candidate Agent Run Queue items
- recommendation on whether the current control-tower shape is enough

### Then: Selected-project run validation

Pick one project and one bounded run.

Validate that the run can start from:

- Project Control Tower record
- Agent Run Queue item
- declared repo read path
- declared write-back targets

The run is not closed until repo state, Notion write-back status, review need,
and follow-up need are recorded.

### Then: Decide on parallel streams

Use observed friction to decide whether to add:

- no new object
- a lightweight stream field
- a first-class Project Streams database/file

Do not decide this only from conceptual design.

## Later roadmap

### Model routing

Add a small model-routing policy that explains:

- cheap/local model tasks
- mid-tier model tasks
- strong model tasks
- coding-agent tasks
- escalation triggers

Avoid building a large routing matrix before the workflow is used.

### Stage skills

Add stage skills only when the base orchestration loop works.

Candidate skills:

- opportunity-frame
- solution-shape
- prototype
- mvp-build
- pilot-connect
- operational-harden
- commercialize
- live-iterate

Each skill should be narrow, task-oriented, and compatible with small read paths.

### Automation and concurrency

Possible future work:

- branch/worktree conventions
- run ownership and lock rules
- collision detection
- automatic repo/Notion reconciliation checks
- scheduled project sweeps
- background status summaries

This remains deferred until the manual control-plane semantics are proven.

## Deferred or explicitly avoided

LLM-OS should not become:

- a full backlog manager
- a general PM tool
- a large multi-agent persona system
- a replacement for Codex or Claude Code
- a workflow runtime before the manual state model is validated
- a duplicate execution plan in Notion

## Review rule

Update this roadmap when:

- the active milestone changes materially
- a decision point is resolved
- a compatibility-impacting version changes the roadmap
- real project use invalidates an assumption

Do not update this roadmap for wording cleanup, minor examples, or historical
notes. Those belong in the relevant local docs or version log.

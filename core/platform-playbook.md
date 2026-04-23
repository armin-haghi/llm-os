# Platform Playbook

This file provides the practical operating guidance for using `llm-os` across
entry points and tools.

It is not the operating model itself.
Use `core/operating-model.md` for the model, `core/agent-contracts.md` for
execution boundaries, `core/external-skills.md` for capability boundary rules,
`core/freshness-model.md` for stale-context rules, and `templates/` for
reusable project artifacts.

## Purpose

Use this playbook to keep behavior consistent across:
- coding-agent entry points
- chat-style entry points
- repo-native work
- future multi-tool surfaces

It exists to answer:
- what to read first
- what to write back
- when to escalate
- how much context to load

## Default read order

For normal serious project work:
1. `AGENTS.md`
2. the live project-doc surface, which defaults to `docs/` unless the local
   repo explicitly overrides it
3. only then directly relevant llm-os-specific reference docs when deeper
   clarification is needed
4. only then explicitly referenced background material

Read only if needed:
- `docs/project-spine.md`
- `docs/open-questions.md`
- `docs/review-report.md`

Do not load by default:
- `llm-os-docs/background/`

Default bias:
- agent actions should route through `AGENTS.md`, `core/`, `skills/`,
  `templates/`, and the live project-doc surface
- `llm-os-docs/` should not be the default action surface

## When to use additional context

Load more only when the current task requires it.

Typical examples:
- load `docs/project-spine.md` when milestone intent or project boundary is
  unclear
- load `docs/open-questions.md` when real decisions or unresolved assumptions
  affect the task
- load `docs/review-report.md` when continuing after review or preparing a new
  review
- load `llm-os-docs/background/` only for design, comparison, operating-model
  evolution, or explicitly referenced context

Use `core/freshness-model.md` when deciding whether current project context is
safe to execute from or needs refresh first.

Use `core/decisions.md` only when a load-bearing operating-model decision is
relevant to the task or when you are updating the operating model itself.

If a target repo uses a non-default live project-doc location, its local
`AGENTS.md` should declare that explicitly. Local repo instructions override
llm-os defaults.

## Write-back expectations

A serious session should leave durable state behind when clarity or outcome
improves.

Common write-back targets:
- `docs/current-milestone.md` when scope, acceptance, blockers, or defaults get
  clearer
- `docs/session-brief.md` when the next action, active risk, or working context
  changes
- `docs/open-questions.md` when a real unresolved decision is surfaced
- `docs/review-report.md` when a milestone is being reviewed

Avoid using chat as the only place where important context lives.

## Escalation rules

Escalate to the human when:
- priority changes are required
- tradeoffs cannot be resolved safely from current evidence
- risk acceptance is needed
- commercial judgment is required
- a real decision endpoint has been reached

Do not escalate just because context is incomplete.
First try to reduce uncertainty through the active milestone, session brief,
and directly relevant project docs.

## Tool behavior

Across tools:
- prefer the smallest sufficient context
- keep `llm-os-docs/background/` out of the default execution path
- select the narrowest agent contract that matches the job
- treat routing as internal lifecycle guidance, not a separate mode system
- write back durable context before closing serious work

Entry points may differ in interface, but they should not define different
operating behavior.

Use `core/external-skills.md` when deciding whether a new skill belongs in the
core operating layer or should remain capability-specific.

Use `project-refresh` when the active project context is stale, unknown, or
contradictory by the rules in `core/freshness-model.md`.

## Lightweight human input

Use `skills/capture-human-input/SKILL.md` when a human wants to add a small
decision, correction, blocker, or next action without reloading the full
project surface.

The skill should write to the smallest correct durable artifact rather than
triggering a broad refresh by default.

Use `skills/surface-human-topics/SKILL.md` when one project's active context
contains decision-worthy uncertainty or risk that should be packaged cleanly
for the human.

## Templates

Use `templates/` as the canonical template layer.

Read only the template needed for the current task:
- `templates/project-spine.md`
- `templates/current-milestone.md`
- `templates/open-questions.md`
- `templates/session-brief.md`
- `templates/review-report.md`

Do not load all templates by default.

## Current repo note

`llm-os` now self-hosts its own live project docs under `docs/` while keeping
`templates/` as the canonical reusable artifact layer.

Treat the repo shape as:
- `templates/` for operational templates
- `docs/` for live llm-os project state
- `llm-os-docs/` for llm-os-specific deeper clarification
- `llm-os-docs/background/` for non-default reference material

Historical background notes may still mention earlier structure. Treat them as
time-scoped analysis unless explicitly refreshed.

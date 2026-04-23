---
name: surface-human-topics
description: Surface decision-worthy and uncertainty-heavy topics inside one project's active context.
---

# Surface Human Topics

Use this skill to turn project-local ambiguity, risk, and decision pressure
into a concise set of human-facing topics.

This skill is project-local.
It does not aggregate across multiple projects.

## Read order

Use the repo's live project-doc surface.
The default layout is `docs/`, but follow any repo-local override declared in
`AGENTS.md`.

Read only the smallest sufficient project context:
1. `session-brief.md` on the live project-doc surface
2. `current-milestone.md` on the live project-doc surface
3. `open-questions.md` on the live project-doc surface only if needed
4. `project-spine.md` on the live project-doc surface only if milestone intent or project boundary is
   unclear

Do not load broad context by default.
Do not load broad background material unless the topic explicitly depends on
design or operating-model reference material.
In `llm-os`, that means `llm-os-docs/background/`.

## What to surface

Surface only items that are genuinely decision-worthy or likely to block safe
execution.

Each surfaced topic should include:
- project
- stage
- active milestone
- recommendation
- uncertainty
- risks
- explicit question for the human
- default next step if the human does not immediately respond

Good candidates:
- unresolved tradeoffs
- assumptions that could change milestone outcome
- blockers that now need human resolution
- scope or priority questions that can no longer be handled safely by default

Do not surface routine implementation details that can be handled locally.

## Write-back behavior

Write to the smallest correct durable artifact.

Typical targets:
- `open-questions.md` on the live project-doc surface when a real human decision or unresolved tradeoff
  needs an owner and default assumption
- `session-brief.md` on the live project-doc surface when the topic mainly affects the current working
  context, next action, or immediate risk framing
- `current-milestone.md` on the live project-doc surface only when the surfaced topic materially changes
  milestone scope, acceptance, dependency framing, or blocker wording

Avoid duplicating the same surfaced topic across multiple artifacts unless the
repo's rules clearly require it.

## Behavior

- keep the output concise and decision-oriented
- prefer one clearly framed human topic over a long list of weak questions
- make the default assumption explicit when safe
- separate uncertainty from actual human decisions
- prefer project-local clarity over portfolio-style rollups

## Escalation

Escalate or request broader context only when:
- the project boundary itself is unclear
- the correct write-back target cannot be chosen safely
- the topic depends on cross-project prioritization
- the current project context is too stale or contradictory to surface topics
  responsibly

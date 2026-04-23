# External Skills Boundary

This file defines the boundary between core `llm-os` behavior and
capability-specific skills.

## Purpose

Use this boundary to keep `llm-os` small and prevent the core from absorbing
tool-, domain-, or workflow-specific logic.

`llm-os` should define how work is operated.
It should not try to encode every capability that might be used inside that
operating model.

## Core belongs in `llm-os` when it defines

- the operating model itself
- stage, milestone, task, lane, and agent-contract behavior
- read-path rules
- write-back expectations
- escalation behavior
- reusable operating templates
- cross-tool guidance that should stay true regardless of domain

Typical homes:
- `core/`
- `templates/`
- entry-surface guidance in `AGENTS.md`
- generic operating skills in `skills/`

## A skill is external when it is primarily about

- a domain capability
- a provider or tool integration
- a product-specific workflow
- a specialized analysis technique
- an implementation pattern that does not belong in every project

Examples:
- vendor- or API-specific integrations
- project-specific build or deploy helpers
- domain-specific planning or review flows
- specialized research or extraction workflows

## Promotion rule

Do not promote a capability-specific skill into the core just because it is
useful once.

Promote only when the pattern:
- is reused across projects
- reduces confusion or decision load
- remains meaningfully tool- and domain-agnostic after abstraction

If abstraction strips away the actual usefulness, keep the skill external.

## Integration rule

External skills may operate inside `llm-os`, but they should not redefine:
- the read path
- the write-back model
- the role of the human as decision endpoint
- the stage / milestone / task / lane model
- the core routing discipline

They plug into the operating model rather than replacing it.

## Practical default

When adding a new skill, ask:
1. is this teaching the system how to operate?
2. or is this teaching the system how to do a specific kind of work?

If the answer is "a specific kind of work," keep it external unless proven
otherwise.

## Current repo note

The current repo skills are still core-facing because they primarily support:
- project refresh
- review gating
- portfolio refresh
- lightweight human input
- human-topic surfacing

If future skills become provider-, domain-, or product-specific, keep them
outside the core operating layer and treat them as external integrations.

Early-stage shaping skills can still live in this repo without becoming core.
Examples include opportunity-analysis or personal-project planning skills.
When they are present, treat them as external or candidate stage skills that
plug into the `llm-os` operating model and write back into the canonical
project docs.

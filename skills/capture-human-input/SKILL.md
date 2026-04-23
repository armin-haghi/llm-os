---
name: capture-human-input
description: Capture lightweight human input and write it to the smallest correct durable artifact.
---

# Capture Human Input

Use this skill when a human wants to add a decision, clarification, blocker,
next action, or scoped correction without reloading full project context.

## Read order

Read only the smallest sufficient context:
1. the human input itself
2. `AGENTS.md` only if the repo's write-back surface is unclear
3. the smallest relevant durable artifact that should receive the update

Do not load broad context by default.
Do not load background/reference material unless the input explicitly depends on
it.

## Write-back target selection

Write to the smallest correct durable artifact.

Typical targets:
- session brief / active work surface for:
  - next action
  - current working context
  - immediate blocker
  - short correction that does not change milestone scope
- current milestone / milestone surface for:
  - scope changes
  - acceptance changes
  - dependency changes
  - blocker changes that affect milestone completion
- open questions / decision surface for:
  - unresolved decisions
  - default assumptions that need an owner
  - explicit human decision points

If the repo defines non-`docs/` action surfaces, use those instead of forcing
the update into `docs/`.

## Behavior

- keep the interaction lightweight
- avoid forcing a full milestone reload when a narrower write-back is enough
- preserve the human's meaning while tightening wording for durability
- prefer one clean write-back target over duplicating the same input across
  multiple files
- mirror into a second artifact only when the repo's rules clearly require it

## Escalation

Escalate or request a broader pass only when:
- the input changes project priority
- the input changes milestone direction materially
- the correct write-back target cannot be chosen safely from local context
- the input creates a real decision package rather than a simple update

If the input is ambiguous but harmless, prefer the most local durable surface
instead of escalating immediately.

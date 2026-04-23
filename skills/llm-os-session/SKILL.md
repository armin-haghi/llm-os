---
name: llm-os-session
description: >
  Start or continue work using the llm-os canonical core. This skill keeps all
  active work centered on the current milestone surface with stage/lane clarity.
---

# LLM-OS Session Skill (Canonical Core)

## Canonical files (read first)
1. `core/operating-model.md`
2. `core/role-contracts.md`
3. `core/change-policy.md`
4. `core/templates/minimal.md`

If any are missing, state the gap and continue with the nearest canonical file.

## Default artifact surface
`docs/current-milestone.md` is the default and should be updated every substantial session.

## Step 1 — Determine mode
- `new-project`
- `existing-project`
- `ongoing-session`

If unclear, ask one short question.

## Step 2 — Load minimum context
1. `docs/current-milestone.md` (create from canonical template if missing)
2. directly linked docs needed for the current task
3. legacy docs only for migration/compatibility

## Step 3 — Execute using stage/lane model
- Place work in the current stage: Scope, Plan, Build, Review, or Ship / Track.
- Assign each non-trivial task to one lane: Human, Build agent, or Review agent.
- Track progress in the milestone task board.

Mode guidance:
- **new-project**: initialize milestone objective, success criteria, first staged tasks.
- **existing-project**: map current work into stage/lane form without rewriting everything.
- **ongoing-session**: advance current staged tasks and define next transition condition.

## Step 4 — Enforce write-back
Write outcomes to `docs/current-milestone.md` by default.
Only add secondary artifacts when milestone clarity requires it.

## Session close block
```md
## Session Close

**Stage advanced:**

**Lane updates (Human / Build agent / Review agent):**

**Tasks changed:**

**Next transition condition:**

**Write-back target:** `docs/current-milestone.md`
```

## Guardrails
- No parallel operating models from legacy docs.
- No transcript-only memory.
- Keep process minimal while preserving milestone clarity.

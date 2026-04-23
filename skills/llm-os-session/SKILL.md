---
name: llm-os-session
description: >
  Start or continue work using the llm-os minimal core. Use when the user asks
  to start a project, continue a project session, or organize ongoing work with
  llm-os conventions.
---

# LLM-OS Session Skill (Minimal Core)

Use this skill to run project sessions against the canonical minimal core.

## Canonical files (read first)
1. `core/operating-model.md`
2. `core/role-contracts.md`
3. `core/change-policy.md`
4. `core/templates/minimal.md`

If any are missing, state the gap and continue with the closest available core file.

## Step 1 — Determine mode
Choose one mode:
- `new-project`: idea-stage or no durable project docs yet
- `existing-project`: active project migrating onto llm-os
- `ongoing-session`: project already has durable docs and active threads

If unclear, ask one short clarification question.

## Step 2 — Load minimum context
- Always read only the smallest needed set.
- Prioritize durable docs over chat history.
- Prefer links/summaries over long transcript restatements.

Default order:
1. `docs/START_HERE.md` (if present)
2. `docs/project-spine.md` (if present)
3. one active doc (`current-milestone`, `active-build`, or `active-review`)
4. only directly relevant references

## Step 3 — Execute by mode
### new-project
- Draft minimal `project-spine` + `current-milestone`
- Surface assumptions, risks, and first execution slice

### existing-project
- Propose migration overlay, not rewrite-everything
- Keep old docs as compatibility shims where useful
- Identify which artifacts become canonical after migration

### ongoing-session
- Continue from durable next steps
- Resolve one priority slice
- Flag drift across Notion/repo docs/GitHub

## Step 4 — Enforce change policy
Promote outcomes only through canonical write-back targets defined in `core/change-policy.md`.

## Session close block
```md
## Session Close

**What we did:**

**Decisions made:**

**Next steps:**

**Write-back targets:**
```

## Guardrails
- No parallel operating model definitions in session output.
- No transcript-as-memory behavior without promotion.
- No unnecessary process overhead; stay minimal and actionable.

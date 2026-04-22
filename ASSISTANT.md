# Assistant Entrypoint (Core-First)

If this file is shared with you, run the session on the **minimal core**.

## Canonical read order
1. `core/operating-model.md`
2. `core/role-contracts.md`
3. `core/change-policy.md`
4. `core/templates/minimal.md`

Treat these as authoritative over legacy docs and chat history.

## Required behavior
- Determine mode: `new-project`, `existing-project`, or `ongoing-session`.
- Keep context minimal: only load what is needed to complete the current step.
- Use minimal templates first; expand only when necessary.
- Route durable outcomes through canonical write-back targets.
- Flag drift when Notion, repo docs, and GitHub disagree.

## Mode outputs
### new-project
- Draft `docs/project-spine.md`
- Draft `docs/current-milestone.md`
- List top assumptions to validate

### existing-project
- Propose smallest migration overlay
- Map existing artifacts to core structure
- Identify what can remain as compatibility shims

### ongoing-session
- Continue from active doc(s)
- Execute one scoped next action
- End with concrete write-back targets

## Session close format
- What changed
- Decisions made
- Next steps
- Write-back target(s)

## Legacy handling
Legacy docs may be referenced for migration context only.
Do not treat them as parallel policy sources.

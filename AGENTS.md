# AGENTS.md

This is the single entrypoint for working with `llm-os`.

## Canonical core
Read these first when entering or modifying the operating model itself:
1. `core/operating-model.md`
2. `core/agent-contracts.md`
3. `core/templates/minimal.md`
4. `core/change-policy.md` only when changing llm-os

## Read paths

### Bootstrap path
Use when:
- entering the repo for the first time
- changing llm-os itself
- setting up a new platform or skill

Read:
1. `core/operating-model.md`
2. `core/agent-contracts.md`
3. `core/templates/minimal.md`
4. `core/change-policy.md` only if the operating model is being changed

### Session path
Use for serious project work.

Read:
1. `docs/session-brief.md`
2. `docs/current-milestone.md`

Read only if needed:
3. `docs/project-spine.md`
4. `docs/open-questions.md`
5. `docs/review-report.md`

## Modes
Determine one mode before proceeding:
- `new-project`: initialize the canonical docs and first milestone
- `existing-project`: load current docs, align context to the canonical surface, then execute
- `ongoing-session`: reload only the active milestone context and the smallest relevant references
- `operating-model-update`: change llm-os itself, using the core files and change policy as the primary context

If unclear, ask one short clarification question.

## Required behavior
- use the smallest sufficient context
- prefer canonical docs over chat history
- invoke the narrow agent contract that matches the task
- improve milestone clarity while doing the work
- end with explicit write-back targets or completed write-backs
- escalate only residual human decisions

## Session close
End serious sessions with:
- what changed
- decisions made
- next steps
- write-back targets

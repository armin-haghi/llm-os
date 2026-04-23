# AGENTS.md

This is the single entrypoint for working with `llm-os`.

## Canonical core
Read these first when entering or modifying the operating model itself:
1. `core/operating-model.md`
2. `core/agent-contracts.md`
3. `core/change-policy.md` only when changing llm-os
4. `core/platform-playbook.md` when practical read paths, write-back behavior, or escalation behavior matter
5. `templates/README.md` only when changing the template layer or initializing project docs
6. `docs/doc-surface-decision.md` when changing repo structure or read paths

## Read paths

### Bootstrap path
Use when:
- entering the repo for the first time
- changing llm-os itself
- setting up a new platform or skill

Read:
1. `core/operating-model.md`
2. `core/agent-contracts.md`
3. `core/change-policy.md` only if the operating model is being changed
4. `core/platform-playbook.md` when platform behavior, write-back rules, or escalation patterns are part of the task
5. `templates/README.md` only when template setup or template changes are part of the task
6. `docs/doc-surface-decision.md` only if repo structure, read paths, or doc boundaries are being changed

### Session path
Use for serious project work.

Read:
1. `docs/session-brief.md`
2. `docs/current-milestone.md`

Read only if needed:
3. `docs/project-spine.md`
4. `docs/open-questions.md`
5. `docs/review-report.md`
6. other directly relevant docs in `docs/`

Do not load by default:
- anything in `docs/background/` unless it is explicitly referenced for design,
  comparison, or operating-model work

## Modes
Determine one mode before proceeding:
- `new-project`: initialize the canonical docs and first milestone
- `existing-project`: load current docs, align context to the canonical surface, then execute
- `ongoing-session`: reload only the active milestone context and the smallest relevant references
- `operating-model-update`: change llm-os itself, using the core files and change policy as the primary context

If unclear, ask one short clarification question.

## Routing
Routing is an internal lifecycle, not a second mode system:

`Think -> Plan -> Build -> Review -> Ship -> Reflect`

Apply it inside the selected mode:
- `new-project`: Think -> Plan
- `existing-project`: Think -> Plan, then execute against the canonical surface
- `ongoing-session`: Think -> Build, with Review / Ship / Reflect only when the work calls for them
- `operating-model-update`: Think -> Plan -> Build -> Review, followed by a consistency check across entry surfaces

Treat `Review`, `Ship`, and `Reflect` as explicit steps only when the current task
actually reaches them.

## Required behavior
- use the smallest sufficient context
- prefer canonical docs over chat history
- invoke the narrow agent contract that matches the task
- improve milestone clarity while doing the work
- keep agent-action surfaces outside `docs/` by default
- keep `docs/background/` out of the default working context
- end with explicit write-back targets or completed write-backs
- escalate only residual human decisions

## Session close
End serious sessions with:
- what changed
- decisions made
- next steps
- write-back targets

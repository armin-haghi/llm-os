# AGENTS.md

This is the single entrypoint for working with `llm-os`.

## Canonical core
Read these first when entering or modifying the operating model itself:
1. `core/operating-model.md`
2. `core/agent-contracts.md`
3. `core/change-policy.md` only when changing llm-os
4. `core/platform-playbook.md` when practical read paths, write-back behavior, or escalation behavior matter
5. `core/decisions.md` only when a load-bearing operating-model decision is relevant
6. `templates/README.md` only when changing the template layer or initializing project docs
7. `llm-os-docs/doc-surface-decision.md` when changing repo structure or read paths

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
5. `core/decisions.md` only when a load-bearing operating-model decision is relevant
6. `templates/README.md` only when template setup or template changes are part of the task
7. `llm-os-docs/doc-surface-decision.md` only if repo structure, read paths, or doc boundaries are being changed

### Session path
Use for serious project work.

Read:
1. `llm-os-docs/project/session-brief.md`
2. `llm-os-docs/project/current-milestone.md`

Read only if needed:
3. `llm-os-docs/project/project-spine.md`
4. `llm-os-docs/project/open-questions.md`
5. `llm-os-docs/project/review-report.md`
6. other directly relevant docs in `llm-os-docs/`

Do not load by default:
- anything in `llm-os-docs/background/` unless it is explicitly referenced for design,
  comparison, or operating-model work

Default assumption for consuming repos:
- the live project-doc surface is `docs/`

Current repo override:
- in `llm-os`, the live project-doc surface is `llm-os-docs/project/`

Override rule:
- if a target repo uses a different live project-doc location, its local
  `AGENTS.md` must declare that explicitly
- any other target-repo overrides from llm-os defaults should also be declared
  locally
- local repo instructions override llm-os defaults

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
- treat `llm-os-docs/project/` as this repo's live project-doc surface
- treat `docs/` as the default live project-doc surface only for consuming repos unless the local repo overrides it
- keep `llm-os-docs/background/` out of the default working context
- end with explicit write-back targets or completed write-backs
- escalate only residual human decisions

## Session close
End serious sessions with:
- what changed
- decisions made
- next steps
- write-back targets

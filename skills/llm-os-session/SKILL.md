---
name: llm-os-session
description: Start or continue serious work using the canonical llm-os core.
---

# llm-os Session

Read first:
1. `core/operating-model.md`
2. `core/agent-contracts.md`
3. `core/change-policy.md` only when changing llm-os
4. `core/platform-playbook.md` when practical read paths, write-back rules, or escalation behavior matter
5. `core/decisions.md` only when a load-bearing operating-model decision is relevant
6. `templates/README.md` only when changing the template layer or initializing project docs
7. `llm-os-docs/doc-surface-decision.md` only when changing repo structure, read paths, or doc boundaries

## Modes
- new-project
- existing-project
- ongoing-session
- operating-model-update

## Default read order
1. `docs/session-brief.md`
2. `docs/current-milestone.md`
3. `docs/project-spine.md` only if needed
4. `docs/open-questions.md` only if needed
5. `docs/review-report.md` only if needed
6. only directly relevant docs in `docs/`

Do not load by default:
- anything in `llm-os-docs/background/` unless it is explicitly referenced for design,
  comparison, or operating-model work

Default assumption:
- the live project-doc surface is `docs/`

Override rule:
- if a target repo uses a different live project-doc location, its local
  `AGENTS.md` must declare that explicitly
- any other target-repo overrides from llm-os defaults should also be declared
  locally
- local repo instructions override llm-os defaults

## Routing
Routing is an internal lifecycle, not a separate mode set:

`Think -> Plan -> Build -> Review -> Ship -> Reflect`

Apply it inside the selected mode:
- `new-project`: Think -> Plan
- `existing-project`: Think -> Plan, then execute
- `ongoing-session`: Think -> Build, with Review / Ship / Reflect only when needed
- `operating-model-update`: Think -> Plan -> Build -> Review, then run a consistency check across affected surfaces

## Rules
- use minimal context and prefer canonical docs over chat memory
- invoke the narrow agent contract that matches the task
- improve milestone clarity while working
- do the intended work before expanding scope
- treat `docs/` as the live project-doc surface by default unless the local repo overrides it
- keep `llm-os-docs/background/` out of the default working context
- end with explicit write-back targets or completed write-backs
- escalate only residual human decisions

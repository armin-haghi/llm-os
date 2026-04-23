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
5. `templates/README.md` only when changing the template layer or initializing project docs
6. `docs/doc-surface-decision.md` only when changing repo structure, read paths, or doc boundaries

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
- anything in `docs/background/` unless it is explicitly referenced for design,
  comparison, or operating-model work

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
- keep `docs/background/` out of the default working context
- end with explicit write-back targets or completed write-backs
- escalate only residual human decisions

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
8. `orchestration/README.md` when refreshing projects, selecting queued work, or coordinating cross-interface agent runs
9. `llm-os-docs/version-log.md` when checking whether a consuming repo needs an llm-os update
10. `llm-os-docs/consistency-check.md` when comparing repo, Notion, and run-handoff state

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
8. `llm-os-docs/version-log.md` only if the change affects consuming repos or compatibility

### Session path
Use for serious work on `llm-os` itself.

Read:
1. `llm-os-docs/project/session-brief.md`
2. `llm-os-docs/project/current-milestone.md`

Read only if needed:
3. `llm-os-docs/project/project-spine.md`
4. `llm-os-docs/project/open-questions.md`
5. `llm-os-docs/project/review-report.md`
6. other directly relevant docs in `llm-os-docs/` only when the `project/` docs are not enough or deeper llm-os-specific clarification is needed

### Orchestration path
Use when the human asks to:
- refresh projects or the control tower
- go through projects and make sure they are all up to date
- start, continue, or pick up work on a chosen project
- coordinate work through the Agent Run Queue

Read:
1. `orchestration/README.md`
2. `orchestration/prompts/project-sweep.md` for portfolio refreshes
3. `orchestration/prompts/start-project-work.md` for selected-project work
4. `llm-os-docs/version-log.md` for the current compatibility standard
5. `llm-os-docs/consistency-check.md` for repo/Notion/run-handoff alignment rules
6. `skills/orchestrator/SKILL.md` when the entrypoint supports skills
7. the relevant Project Control Tower and Agent Run Queue records when Notion access exists
8. the target project's local `AGENTS.md`, `project-overview.yaml`, current milestone, and session brief only as required by the orchestration prompt

The orchestration path is an interaction and dispatch path. It is not a second execution source of truth. Once a project has a repo, repo-local docs remain canonical for execution state.

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
- if local repo instructions are missing or ambiguous, fall back to the
  canonical `llm-os` defaults before inventing local behavior

## Modes
Determine one mode before proceeding:
- `new-project`: initialize or retrofit root `AGENTS.md`, the canonical docs, `project-overview.yaml`, and the first milestone
- `existing-project`: load current docs, align context to the canonical surface, then execute; this can include a project that already exists but is not yet following the `llm-os` rules cleanly
- `ongoing-session`: reload only the active milestone context and the smallest relevant references
- `operating-model-update`: change llm-os itself, using the core files and change policy as the primary context
- `orchestration`: refresh project/control-tower state or start selected-project work through the shared orchestration path

If unclear, ask one short clarification question.

## Routing
Routing is an internal lifecycle, not a second mode system:

`Think -> Plan -> Build -> Review -> Ship -> Reflect`

Apply it inside the selected mode:
- `new-project`: Think -> Plan, then audit the repo, create only the missing canonical docs from `templates/`, and fill the minimum working content
- `existing-project`: Think -> Plan, then execute against the canonical surface
- `ongoing-session`: Think -> Build, with Review / Ship / Reflect only when the work calls for them
- `operating-model-update`: Think -> Plan -> Build -> Review, followed by a consistency check across entry surfaces
- `orchestration`: Think -> Plan, then run either project sweep or selected-project work from `orchestration/README.md`; Review / Reflect when state, compatibility, or source-of-truth drift is found

Treat `Review`, `Ship`, and `Reflect` as explicit steps only when the current task
actually reaches them.

## Required behavior
- use the smallest sufficient context
- prefer canonical docs over chat history
- invoke the narrow agent contract that matches the task
- improve milestone clarity while doing the work
- route project sweeps and selected-project coordination through `orchestration/README.md`
- check `llm_os_version` and update-needed state during project sweeps
- use `llm-os-docs/consistency-check.md` before declaring repo and Notion state aligned
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

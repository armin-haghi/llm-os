# llm-os — Minimal Core First

This repository now uses a **minimal core** model.

## Canonical operating model
Use these files as the single source of truth:
- `core/operating-model.md`
- `core/role-contracts.md`
- `core/change-policy.md`
- `core/templates/minimal.md`

Everything else should either:
1) apply the core to a specific workflow, or
2) serve as a compatibility/migration shim.

## Entry surfaces
- `ASSISTANT.md` — assistant-facing boot contract
- `skills/llm-os-session/SKILL.md` — session orchestration skill for agents
- `AGENTS.md` — root coding-agent anchor for this repo

## Migration stance
Older documents are retained only to ease adoption and transition.
They must not define a competing operating model.

## Practical default
When in doubt:
1. read the core files
2. choose one role contract
3. execute one scoped task
4. promote outcomes using `core/change-policy.md`

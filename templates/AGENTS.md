# AGENTS.md

This is the single entrypoint for working with this repo under `llm-os`.

## Read path

For normal serious project work, read:
1. `docs/session-brief.md`
2. `docs/current-milestone.md`

Read only if needed:
3. `docs/project-spine.md`
4. `docs/open-questions.md`
5. `docs/review-report.md`

## Modes
Determine one mode before proceeding:
- `new-project`: initialize or retrofit this repo's operating surface, `project-overview.yaml`, and first milestone
- `existing-project`: load current docs, align context, then execute; this can include a repo that already exists but is not yet following the `llm-os` rules cleanly
- `ongoing-session`: reload only the active milestone context and the smallest relevant references

If unclear, ask one short clarification question.

## Routing
Routing is an internal lifecycle:

`Think -> Plan -> Build -> Review -> Ship -> Reflect`

Apply it inside the selected mode:
- `new-project`: Think -> Plan, then audit the repo, create only the missing canonical docs, and fill the minimum working content
- `existing-project`: Think -> Plan, then execute against the live project-doc surface
- `ongoing-session`: Think -> Build, with Review / Ship / Reflect only when needed

## Required behavior
- use the smallest sufficient context
- prefer canonical docs over chat history
- treat `docs/` as the live project-doc surface unless this repo declares a local override
- keep important context in repo docs, not only in chat
- improve milestone clarity while doing the work
- end with explicit write-back targets or completed write-backs
- escalate only residual human decisions

# Orchestration Prompt: Project Audit

Use this when the human says:

> Audit this project for LLM-OS gaps.

or:

> Is this project ready for LLM-OS orchestration?

## Role

You are the project-readiness auditor for `llm-os`.

Your job is to determine whether one project can be safely run through the
`llm-os` orchestration path without the human manually reconstructing context.

This is not a full project review, product critique, or implementation review.
It is a conformance and readiness check for the operating surface.

## Inputs

Required:
1. chosen project name
2. Project Control Tower record for that project, when available
3. Agent Run Queue records for that project, when available
4. repo `AGENTS.md` or equivalent project entrypoint, when a repo exists
5. repo `project-overview.yaml`, when a repo exists
6. repo current milestone and session brief, when a repo exists
7. canonical `llm-os` `llm-os-docs/version-log.md`
8. canonical `llm-os` `llm-os-docs/consistency-check.md`

Optional:
- open questions or decisions file
- review report
- active PR or issue only if referenced by the run or milestone

Known Notion surfaces:
- Project Control Tower:
  private Notion database named `Project Control Tower`
- Agent Run Queue:
  private Notion database named `Agent Run Queue`

Resolve Notion surfaces by name through the Notion connector when available.
If Notion access is unavailable, use `.llm-os.local.yaml` locally or ask the
human for the private surface links/access.

## Audit checks

Score each check as `pass`, `warn`, `fail`, or `unknown`.

### 1. Entrypoint

Check whether the project has a clear repo entrypoint:

- root `AGENTS.md`, or
- equivalent local instructions declared in the repo, or
- clear Notion-only working surface for pre-repo projects

Pass when an agent can determine the local read path without asking the human to
reconstruct context.

### 2. Project state

Check whether the project has a current state record:

- project name
- status
- stage
- active milestone
- freshness
- last reviewed date
- owner
- blocker
- next decision
- next action
- canonical repo or Notion page
- execution surface

For repo-backed projects, prefer `project-overview.yaml` as the rollup input.
For pre-repo projects, use the canonical Notion page and control-tower record.

### 3. Milestone clarity

Check whether the active milestone has:

- goal
- why it matters
- in-scope work
- out-of-scope work
- acceptance criteria or done condition
- blocker, if any
- next action

Warn if the milestone exists but is too vague for an agent to start.
Fail if no active milestone can be found.

### 4. Run readiness

Check whether there is a bounded Agent Run Queue item or enough state to create
one.

A ready run needs:

- bounded goal
- input source
- required read path
- write-back targets
- clear status
- human decision or `none`

Classify the project as blocked if the run is good but depends on a named human
input, credential, deploy value, or risk decision.

### 5. Human decisions

Check whether unresolved decisions are explicit.

Pass when the project names the current decision or says `none`.
Warn when decisions are implied but not captured.
Fail when an agent cannot tell whether it is allowed to proceed.

### 6. Source-of-truth boundary

Check whether the project clearly separates:

- repo docs as execution truth once a repo exists
- Notion as portfolio, dispatch, blocker, and human-decision layer
- completed run handoffs as historical unless marked latest as of a commit

Use `llm-os-docs/consistency-check.md` for alignment rules.

### 7. Compatibility

Check whether the project follows the current standard in
`llm-os-docs/version-log.md`.

For repo-backed projects, check `project-overview.yaml` for:

- `llm_os_version`
- `llm_os_profile`
- `llm_os_last_checked`
- `llm_os_update_needed`
- `llm_os_update_reason`

Warn or fail if fields are missing, stale, or incompatible with the current
standard.

### 8. Resume quality

Check whether an agent could resume the project without asking the human to
summarize the previous thread.

Pass when the next run or next action can be started from declared context.
Warn when some context is missing but recoverable.
Fail when the human must reconstruct project history before work can continue.

## Readiness classification

Return one overall readiness status:

- `ready`
  - an agent can start or continue a bounded run now
- `blocked`
  - an agent can proceed once a named blocker or human decision is resolved
- `needs-sync`
  - repo, Notion, or run state disagree and must be reconciled first
- `needs-migration`
  - the project is behind the current `llm-os` standard or missing required
    compatibility fields
- `not-ready`
  - the project lacks enough durable state for safe orchestration
- `unknown`
  - required sources are unavailable

Prefer the most specific status. For example, if a project has good structure
but is missing `llm_os_version`, use `needs-migration`. If it has a good run but
awaits a deploy secret, use `blocked`.

## Output format

Return:

1. one short overall assessment
2. a table with each audit check, status, finding, and fix
3. a compact machine-readable summary
4. recommended next action
5. whether to create or update an Agent Run Queue item

Use this machine-readable shape:

```yaml
project: "[project name]"
llm_os_readiness: "[ready|blocked|needs-sync|needs-migration|not-ready|unknown]"
llm_os_version_status: "[current|update-needed|unknown|not-applicable]"
source_of_truth_alignment: "[aligned|repo-newer-than-notion|notion-newer-than-repo|unknown]"
agent_resume_quality: "[good|partial|poor|unknown]"
blocking_decision: "[decision or none]"
recommended_next_action: "[one concrete next action]"
migration_needed: "[yes|no|unknown]"
migration_reason: "[specific reason or none]"
```

## Write-back behavior

Do not modify the project by default.

If the user explicitly asks to apply fixes, write back only safe metadata fixes,
such as:

- missing compatibility fields in `project-overview.yaml`
- stale Project Control Tower freshness or update-needed state
- stale Agent Run Queue status when the run is clearly historical or blocked

For larger fixes, create or recommend one bounded Agent Run Queue item instead
of editing many surfaces at once.

## Rules

- Do not turn the audit into a product critique.
- Do not audit every file in the repo.
- Do not ask the human to summarize project history if the declared read path
  already contains enough information.
- Do not mark a project ready if there is no explicit next action or run.
- Do not treat missing compatibility fields as a fatal project issue; classify
  it as migration or sync work.

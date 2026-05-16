# First Setup

This is the minimum setup needed for an agent to follow the `llm-os` model.

The goal is not to make every tool identical.
The goal is to give every assistant entrypoint the same operating path:

1. use a durable status surface for pre-repo ideas, portfolio state, and agent-run dispatch
2. use repo docs as execution truth once a repo exists
3. write durable state back before closing serious work
4. ask the human only when judgment, access, priority, or risk acceptance is
   actually needed

A status surface may be Notion, Confluence, markdown files, a project tracker,
or another durable workspace. The tool is interchangeable; the operating
contract is not.

## What the agent needs

At minimum, an agent needs:

- access to this `llm-os` repo, or a copy of the relevant setup and
  orchestration docs
- an active assistant interface, such as OpenClaw, Codex, Claude, ChatGPT, or
  another tool that can follow repo instructions
- access to the chosen status surface when the work is pre-repo, portfolio-level,
  or run-queue based
- repo access when the work is implementation or repo-backed project execution

No public repo file should contain private workspace URLs.
Use stable human-readable surface names in tracked docs.

## Private status-surface access

For pre-repo idea expansion and orchestration, the preferred setup is a connector
or integration that can search and update the private workspace. In the current
workspace that surface is usually Notion, but the same pattern can be implemented
with Confluence, markdown, or another tracker.

Expected private status surfaces in the current setup:

- `Project Control Tower`
- `Agent Run Queue`
- one canonical page/document/record per pre-repo idea, business case, or personal project
- project-specific planning pages/documents when they already exist

Resolution order for private status surfaces:

1. search by exact page, database, document, or tracker name through the connector
2. use a mention or link supplied by the human in the current session
3. for local CLI workflows only, read `.llm-os.local.yaml`
4. if none of those are available, ask the human for access or pasted content

`.llm-os.local.yaml` is optional.
It is a local convenience for tools that can read files but cannot search the
private workspace by name.
It is not the main operating model.

## Pre-Repo Ideas

Use this path for idea expansion, business cases, and personal projects before
a repo exists.

Setup:

1. create one canonical status page, document, or record for the idea
2. give it a stable, searchable name
3. keep it private unless it is intentionally shared
4. include or maintain these fields, either as database properties, document
   metadata, frontmatter, a tracker row, or a compact summary block:
   - status
   - stage
   - freshness
   - last reviewed
   - owner
   - next decision
   - next action
   - canonical repo, blank until one exists
   - status-surface link, stored in the private Project Control Tower when useful
   - execution surface, the status surface before a repo exists

Agent behavior:

- read `llm-os-docs/notion-first-ideation.md` for the portable status-surface pattern
- work directly on the canonical status surface when the connector allows it
- use comments or small child docs for review, critique, or appendices
- keep status, freshness, next decision, and next action current
- do not require a repo, GitHub issue, or local env file

If the agent has no access to the chosen status surface, it can draft from
pasted content, but write-back is blocked.

## Repo-Backed Projects

Use this path once a project has a repo or is ready for implementation.

Minimum repo setup:

1. root `AGENTS.md`
2. live project docs, defaulting to `docs/` unless the repo declares an
   override
3. `project-overview.yaml`
4. current milestone and session brief
5. local `.llm-os.local.yaml` only if private links need to be resolved by a
   local tool

Agent behavior:

- read the target repo's `AGENTS.md` first
- follow repo-local read paths and overrides
- treat repo docs as execution truth
- update the external status surface only as summary, run dispatch, feedback, or
  human decision support
- do not keep a competing implementation plan in the external status surface

## Orchestration

Use this path when the human wants an agent to coordinate across projects or
start work from a selected project.

Setup:

1. create or connect the private status surface named `Project Control Tower`
2. create or connect the private status surface named `Agent Run Queue`
3. seed each active project with one project record
4. create one run record per bounded agent session or handoff
5. keep raw private workspace URLs out of tracked public docs

Agent behavior:

- use `orchestration/README.md`
- use `orchestration/prompts/project-sweep.md` to refresh all projects
- use `orchestration/prompts/start-project-work.md` to start a selected
  project
- use `skills/orchestrator/SKILL.md` when a skill entrypoint is available
- use `skills/agent-run/SKILL.md` when picking up one bounded run

The run queue should reduce human thread management.
It should not become a backlog.

## Access Matrix

| Situation | What works | What is blocked |
| --- | --- | --- |
| Status-surface connector available, no repo | pre-repo idea expansion in the status surface | repo implementation |
| Status-surface connector unavailable, no repo | draft from pasted content | status-surface read/write-back |
| Repo access available, no status-surface access | repo-backed execution from local docs | portfolio/run-queue updates |
| Repo and status-surface access available | full model | only human-owned decisions |
| Local CLI with private config | can resolve private links from `.llm-os.local.yaml` | status-surface writes if no connector exists |

## First-Agent Checklist

Before expecting an agent to operate the model, verify:

- it can read this repo or the relevant setup excerpt
- it can access the status surface if the task is pre-repo or orchestration work
- it can access the target repo if the task is implementation work
- it knows whether the current work is pre-repo status-surface work or repo-backed work
- it knows the durable write-back target before starting
- it can ask the human for access instead of pretending blocked context is
  available

If those checks pass, the setup is sufficient.
Do not add more process until a real run shows a missing field or handoff.

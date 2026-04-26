# First Setup

This is the minimum setup needed for an agent to follow the `llm-os` model.

The goal is not to make every tool identical.
The goal is to give every assistant entrypoint the same operating path:

1. use Notion for pre-repo ideas, portfolio state, and agent-run dispatch
2. use repo docs as execution truth once a repo exists
3. write durable state back before closing serious work
4. ask the human only when judgment, access, priority, or risk acceptance is
   actually needed

## What the agent needs

At minimum, an agent needs:

- access to this `llm-os` repo, or a copy of the relevant setup and
  orchestration docs
- an active assistant interface, such as OpenClaw, Codex, Claude, ChatGPT, or
  another tool that can follow repo instructions
- Notion access when the work is pre-repo, portfolio-level, or run-queue based
- repo access when the work is implementation or repo-backed project execution

No public repo file should contain private Notion URLs.
Use stable Notion surface names in tracked docs.

## Private Notion access

For pre-repo idea expansion and orchestration, the preferred setup is a Notion
connector or integration that can search and update the private workspace.

Expected private Notion surfaces:

- `Project Control Tower`
- `Agent Run Queue`
- one canonical page per pre-repo idea, business case, or personal project
- project-specific planning pages when they already exist

Resolution order for private Notion surfaces:

1. search Notion by exact page or database name through the connector
2. use a page mention or link supplied by the human in the current session
3. for local CLI workflows only, read `.llm-os.local.yaml`
4. if none of those are available, ask the human for access or pasted content

`.llm-os.local.yaml` is optional.
It is a local convenience for tools that can read files but cannot search
Notion by name.
It is not the main operating model.

## Pre-Repo Ideas

Use this path for idea expansion, business cases, and personal projects before
a repo exists.

Setup:

1. create one canonical Notion page for the idea
2. give it a stable, searchable name
3. keep the page private unless it is intentionally shared
4. include or maintain these fields, either as database properties or a compact
   summary block:
   - status
   - stage
   - freshness
   - last reviewed
   - owner
   - next decision
   - next action
   - canonical repo, blank until one exists
   - execution surface, `Notion` before a repo exists

Agent behavior:

- read `llm-os-docs/notion-first-ideation.md`
- work directly on the canonical Notion page
- use comments or small child pages for review, critique, or appendices
- keep status, freshness, next decision, and next action current
- do not require a repo, GitHub issue, or local env file

If the agent has no Notion access, it can draft from pasted content, but Notion
write-back is blocked.

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
- update Notion only as summary, run dispatch, feedback, or human decision
  surface
- do not keep a competing implementation plan in Notion

## Orchestration

Use this path when the human wants an agent to coordinate across projects or
start work from a selected project.

Setup:

1. create or connect the private Notion database named `Project Control Tower`
2. create or connect the private Notion database named `Agent Run Queue`
3. seed each active project with one project record
4. create one run record per bounded agent session or handoff
5. keep raw Notion URLs out of tracked public docs

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
| Notion connector available, no repo | pre-repo idea expansion in Notion | repo implementation |
| Notion connector unavailable, no repo | draft from pasted content | Notion read/write-back |
| Repo access available, no Notion | repo-backed execution from local docs | portfolio/run-queue updates |
| Repo and Notion available | full model | only human-owned decisions |
| Local CLI with private config | can resolve private links from `.llm-os.local.yaml` | Notion writes if no Notion tool exists |

## First-Agent Checklist

Before expecting an agent to operate the model, verify:

- it can read this repo or the relevant setup excerpt
- it can access Notion if the task is pre-repo or orchestration work
- it can access the target repo if the task is implementation work
- it knows whether the current work is pre-repo Notion work or repo-backed work
- it knows the durable write-back target before starting
- it can ask the human for access instead of pretending blocked context is
  available

If those checks pass, the setup is sufficient.
Do not add more process until a real run shows a missing field or handoff.

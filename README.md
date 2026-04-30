# llm-os

`llm-os` is a lightweight operating system for building products with multiple
LLM tools, agents, and coding assistants without losing the thread.

It is not a single app, coding agent, or project-management system. It is a
shared way to keep product intent, project state, human decisions, agent
handoffs, and repo write-backs aligned across tools such as ChatGPT, Claude,
Codex, OpenClaw, local models, Notion, and GitHub.

For the fuller explanation, read `llm-os-docs/overview.md`.
For agent instructions, read `AGENTS.md`.

## Why this exists

LLM-assisted work fragments easily:

- ideas stay trapped in chat threads
- plans drift from implementation
- different assistants see different context
- repo docs go stale
- Notion becomes a second plan instead of a control layer
- coding agents finish work but do not update durable project state
- the human has to reconstruct what happened before each next session

That is manageable for one small task. It breaks when multiple projects or
streams are moving in parallel.

`llm-os` exists to make that work durable, visible, and easier to resume.

## What it is trying to achieve

A good `llm-os` setup should let the human ask:

- What projects are active right now?
- Which projects are stale or blocked?
- Which project needs my decision?
- Which work is ready for an agent?
- What can a cheaper model handle?
- What needs a stronger model or coding agent?
- What changed since the last session?
- Which repo or Notion page is the source of truth?
- What is the next useful action?

The answer should come from durable project state, not from memory of a chat.

## The core idea

`llm-os` separates work into clear layers:

1. Human intent
   - the human owns direction, priority, tradeoffs, and risk decisions
2. Project state
   - each project keeps a small durable record of stage, milestone, blocker,
     next action, next decision, freshness, and source of truth
3. Control tower
   - Notion shows portfolio state, blockers, priorities, human decisions, and
     cross-project visibility
4. Agent run queue
   - bounded runs tell agents what to read, what to do, what they may change,
     and where they must write back
5. Repo execution truth
   - once a project has a repo, repo-local docs own execution state

The system should make it possible to move between assistants and still keep the
same operating context.

## How it should feel

The human should be able to say:

> Go through my projects and make sure they are up to date.

An assistant should then refresh project state, detect stale docs, check whether
Notion and repo state disagree, surface real human decisions, and recommend the
next useful run.

The human should also be able to say:

> Start orchestrating work on AlphaGen.

An assistant should then pick or create one bounded run, load only the required
context, execute or dispatch the work, and write back before closing.

## What this repo contains

- `AGENTS.md` — the main operational entrypoint for agents and assistants
- `llm-os-docs/overview.md` — user-facing explanation of the system
- `orchestration/README.md` — shared path for project sweeps and selected-project work
- `llm-os-docs/consistency-check.md` — rules for detecting repo/Notion/run-handoff drift
- `llm-os-docs/version-log.md` — compatibility-impacting changes and migration guidance
- `core/` — operating-model rules, contracts, decisions, and platform behavior
- `templates/` — starter files for adopting `llm-os` in another repo
- `skills/` — task-oriented skills such as initialization, refresh, review, and orchestration
- `llm-os-docs/project/` — this repo's own live project docs

## What it is not

`llm-os` is not:

- a replacement for Codex, Claude Code, OpenClaw, or other coding agents
- a full project-management system
- a task backlog
- a multi-agent runtime
- a prompt library only
- a place to store every conversation
- a heavy methodology that every project must follow in detail

It is the coordination layer around those tools.

## Core rule

A serious session should:

1. load current context
2. do the intended work
3. reduce milestone uncertainty where possible
4. update durable project state when clarity improves
5. check source-of-truth and compatibility drift when working across repo and Notion
6. escalate only residual human decisions

## Start here

- Human overview: `llm-os-docs/overview.md`
- Agent entrypoint: `AGENTS.md`
- Project orchestration: `orchestration/README.md`
- Consistency checks: `llm-os-docs/consistency-check.md`
- Version tracking: `llm-os-docs/version-log.md`

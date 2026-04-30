# What LLM-OS Is About

`llm-os` is a lightweight operating system for building products with multiple
LLM tools, agents, and coding assistants without losing the thread.

It is not a single app, framework, or coding agent. It is a shared way of
organizing product work so a human can move between ChatGPT, Claude, Codex,
OpenClaw, local models, Notion, and GitHub while preserving intent, state,
decisions, and next actions.

## The problem

LLM-assisted work often starts well and then fragments:

- ideas live in chat threads
- plans drift from implementation
- different assistants see different context
- repo docs go stale
- Notion pages become parallel plans
- coding agents complete work but do not update the project state
- the human has to remember what happened and reconstruct context each time

That is manageable for one small task. It breaks down when several products,
experiments, or work streams are moving in parallel.

`llm-os` exists to make that work durable.

## The goal

The goal is to turn product development into a set of bounded, visible,
agent-ready streams of work.

A good `llm-os` setup should let the human ask:

- What projects are active right now?
- Which project needs my decision?
- Which work is ready for an agent?
- What can a cheaper model handle?
- What needs a stronger model or coding agent?
- What changed since the last session?
- Which repo or Notion page is the source of truth?
- What is the next useful action?

The answer should come from durable project state, not from memory of a chat.

## The mental model

`llm-os` separates work into a few clear layers.

### 1. Human intent

The human sets direction, tradeoffs, risk appetite, and priorities.

Agents can propose, critique, build, and summarize, but they should not silently
change product direction or make unresolved judgment calls.

### 2. Project state

Each project has a small durable state surface:

- what the project is
- what stage it is in
- the active milestone
- current blocker
- next action
- next human decision
- freshness
- source of truth

For repo-backed projects, this state lives primarily in the repo.
For pre-repo ideas, one canonical Notion page can be the working surface.

### 3. Control tower

Notion acts as the portfolio view.

It shows the current state across projects, but it should not become a second
implementation plan once a repo exists.

The control tower answers: where should attention go next?

### 4. Agent run queue

The Agent Run Queue turns vague agent work into bounded handoffs.

A run should say:

- what goal to achieve
- what to read
- what can be changed
- where to write back
- what human decision is needed, if any
- what happened when the run is done

The queue is not a task backlog. It is a dispatch and handoff layer for serious
agent sessions.

### 5. Repo execution truth

Once a project has a repo, repo docs are the execution source of truth.

That means implementation state, current milestone, decisions, and acceptance
criteria should be written back to repo-local docs instead of being left in
chat or duplicated in Notion.

## How it should feel in practice

The human should be able to start from any supported assistant and say:

> Go through my projects and make sure they are up to date.

The assistant should then:

1. read the Project Control Tower
2. read relevant repo overview files
3. check freshness and compatibility
4. detect source-of-truth drift
5. update Notion only where it is the portfolio/run layer
6. surface only real human decisions
7. recommend the next useful run

The human should also be able to say:

> Start orchestrating work on AlphaGen.

The assistant should then:

1. load that project's control-tower record
2. find or create one bounded run
3. load only the necessary repo context
4. execute or dispatch the work
5. update the run and repo docs before closing
6. ask the human only for judgment, access, priority, or risk decisions

## What LLM-OS is not

`llm-os` is not:

- a replacement for Codex, Claude Code, OpenClaw, or other coding agents
- a full project-management system
- a backlog tracker
- a multi-agent framework
- a prompt library only
- a place to store every conversation
- a heavy methodology that every project must follow in detail

It is the coordination layer around those tools.

## The key design principles

### Durable state beats chat memory

Important context should be written to repo docs or Notion records. Chat can be
used for working, but not as the only place where project state lives.

### One source of truth per layer

Repo docs own execution state once a repo exists.
Notion owns portfolio state, dispatch state, blockers, and human decisions.
Completed run records are historical unless they explicitly say they are the
latest state as of a commit.

### Small context by default

Agents should load the smallest useful read path. They should not pull every
doc into context unless the task requires it.

### Narrow agents over broad personas

The system favors task contracts such as project refresh, review gate,
portfolio refresh, build, debug, ship, or orchestrator. The goal is not to give
every agent a large personality. The goal is to make each run bounded and
checkable.

### Serious sessions should improve clarity

A serious session should not only produce work. It should also reduce milestone
uncertainty, update durable state, and leave the next session easier to start.

### Cheap models should be useful, but not overtrusted

Smaller or cheaper models can help with intake, summarization, formatting, and
first-pass organization. The system should escalate when the task needs deeper
reasoning, architecture judgment, product tradeoffs, risk acceptance, or code
execution.

## Why versioning matters

`llm-os` itself changes over time.

When the operating model, templates, run queue, or orchestration rules change,
existing projects may need small migrations. The version log and compatibility
fields make that visible.

A project sweep should be able to say:

- this project follows the current standard
- this project is missing new fields
- this project needs an `llm-os` migration run
- this project is pre-repo and should stay Notion-only for now

This avoids silent drift across projects.

## The intended end state

The intended end state is a personal product-development control plane.

The human can run multiple projects in parallel, use different LLM tools for
different jobs, and still preserve:

- product intent
- current state
- active milestone
- human decisions
- agent handoffs
- repo write-backs
- review outcomes
- compatibility with the current operating standard

`llm-os` succeeds when the human spends less time reconstructing context and
more time making the few decisions that actually need human judgment.

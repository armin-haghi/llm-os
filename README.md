# LLM Operating System Starter — Tailored Stack

A repo-ready operating model tailored to this stack:

- **OpenClaw**: idea expansion, exploratory branching, rough option generation
- **Claude / ChatGPT**: synthesis, review, restructuring, comparison, artifact drafting
- **Claude Code / Codex**: implementation planning and code changes
- **Notion**: milestone planning, status, collaboration, comments
- **GitHub**: canonical codebase, technical docs, issues, pull requests

## Stack-specific model

- **Notion is the control tower** for milestones, status, owners, risks, and collaboration.
- **GitHub repo is the technical source of truth** for implementation-ready context.
- **OpenClaw sessions are scratchpads** unless promoted into repo docs or Notion.
- **ChatGPT is the synthesizer/reviewer**, not the only memory layer.
- **Claude Code / Codex are builders** that should read the smallest sufficient technical context.

## Standard workflow

### 1. Explore in OpenClaw
Use OpenClaw to expand an idea, compare directions, or draft a rough plan.

Write back one of:
- `docs/reviews/active-review.md`
- `docs/handoffs/active-build.md`
- a summary section on the relevant Notion milestone page

### 2. Review in ChatGPT or with humans
Use ChatGPT to critique assumptions, simplify plans, compare options, or turn messy notes into a structured artifact.

Write back one of:
- `docs/reviews/active-review.md`
- `docs/current-milestone.md`
- Notion milestone notes / risks / open questions

### 3. Build in Claude Code or Codex
Use the active handoff and only the referenced technical docs.

Write back one of:
- `docs/handoffs/active-build.md`
- `docs/decision-log.md`
- GitHub issue / PR notes

### 4. Track in Notion + GitHub
- Notion tracks milestone progress, blockers, ownership, and comments.
- GitHub tracks execution tasks, issues, PRs, and code-linked status.

## What this package includes

- `principles/operating-model.md`: source-of-truth rules, context budget, routing, and write-back rules
- `INSTRUCTIONS.md`: stack-specific instructions for OpenClaw, ChatGPT, Claude Code / Codex, and lightweight task roles
- `SETUP.md`: suggested Notion database schema and GitHub conventions
- `TEMPLATES.md`: canonical markdown templates for project docs
- `ASSISTANT.md`: single assistant-facing entrypoint designed to be shared as one link
- `skills/llm-os-session/`: agent skill for running lightweight llm-os sessions from canonical context
- `project-scaffold/`: a slim per-project folder structure to copy into a real repo

## Quick Start With ChatGPT or Claude

If you want an assistant to help you apply this system, start by sharing `ASSISTANT.md`.

- Best case: paste only a link to `ASSISTANT.md`
- If useful, add one short line of context such as:
  - `Use this operating model for my new project:`
  - `Use this as a lightweight overlay for my existing project:`
  - `Work in this repo using this operating model:`
- `ASSISTANT.md` is written to handle new projects, existing projects, and ongoing sessions

## Default reading policy by tool

### OpenClaw
1. `docs/START_HERE.md`
2. `docs/project-spine.md`
3. relevant Notion milestone summary or `docs/current-milestone.md`
4. stop unless more is explicitly needed

### ChatGPT
1. `docs/START_HERE.md`
2. `docs/project-spine.md`
3. active milestone, review, or handoff doc
4. at most 2 to 3 relevant supporting docs

### Claude Code / Codex
1. `docs/START_HERE.md`
2. `docs/project-spine.md`
3. `docs/handoffs/active-build.md`
4. only the referenced technical docs
5. `docs/decision-log.md` if ambiguity remains

## Default write-back policy

At the end of each useful session, update only one or more of:

- `docs/decision-log.md`
- `docs/status-update.md`
- `docs/current-milestone.md`
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- the corresponding Notion milestone page
- the relevant GitHub issue or PR description/comment

Do not treat raw chat transcripts as canonical memory.

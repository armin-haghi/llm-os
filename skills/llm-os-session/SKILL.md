---
name: llm-os-session
description: >
  Kicks off or continues a project session using Armin's llm-os operating model
  (https://github.com/armin-haghi/llm-os). Use this skill whenever the user
  pastes a Notion page, mentions a project, says "let's work on X", "continue
  where we left off on X", "start a new project for X", or references next steps
  from a project. Also trigger when the user pastes a Notion URL or block of
  Notion content alongside a project name or task description. This skill
  determines session mode (new-project / existing-project / ongoing-session),
  fetches the live llm-os repo for its canonical rules, reads the Notion context
  provided, supports Claude Code and Codex CLI repo context anchors, and
  produces a scoped session plan with clear next actions.
---

# LLM-OS Session Skill

This skill applies Armin's [llm-os](https://github.com/armin-haghi/llm-os)
operating model to start or continue a project session. It always reads the
**live repo** - never relies on hardcoded rules.

---

## Step 1 - Fetch live repo files

Before doing anything else, fetch these raw files from GitHub:

```
https://raw.githubusercontent.com/armin-haghi/llm-os/main/ASSISTANT.md
https://raw.githubusercontent.com/armin-haghi/llm-os/main/README.md
https://raw.githubusercontent.com/armin-haghi/llm-os/main/INSTRUCTIONS.md
https://raw.githubusercontent.com/armin-haghi/llm-os/main/principles/operating-model.md
```

Use the fetch method available in the current agent:

- Claude Code: use the Bash tool with `curl` to fetch each raw URL.
- Codex CLI: use shell access with `curl` to fetch each raw URL.
- claude.ai: use `web_fetch` on each raw URL in parallel, or sequentially if parallel is unavailable.

If a file 404s, skip it and note the gap. Do **not** fall back to any cached
version of these rules - the whole point is that they evolve.

Optionally fetch if the session calls for it:

```
https://raw.githubusercontent.com/armin-haghi/llm-os/main/TEMPLATES.md
https://raw.githubusercontent.com/armin-haghi/llm-os/main/SETUP.md
```

---

## Step 2 - Read the Notion context

The user will typically paste a Notion page or URL. Handle both cases:

**If a Notion URL is provided:** Use the Notion MCP tool (`notion-fetch`) to
retrieve the page. Add a 3-5 line summary at the top before reading full
content (per Armin's memory preference). Only read the full page if the summary
is insufficient.

**If Notion content is pasted directly:** Use it as-is. Extract:
- Project name
- Current status / last known state
- Next steps or open tasks
- Any blockers or decisions pending

If neither is provided, ask: *"Can you paste the Notion page or URL for this
project?"*

---

## Step 3 - Determine session mode

Using the content from the Notion page + any repo docs available, determine:

| Mode | Signal |
|------|--------|
| `new-project` | No existing docs, idea is raw, user says "start", "new", "build" |
| `existing-project` | Active project but llm-os not yet applied; existing code/Notion but no `docs/` scaffold |
| `ongoing-session` | `docs/START_HERE.md` or `docs/project-spine.md` already exists; user says "continue" |

If unclear, ask **one short question** to resolve.

---

## Step 4 - Execute the mode

### Mode: new-project

Follow `ASSISTANT.md` new-project rules (fetched in Step 1). Produce:

1. Draft `docs/project-spine.md` - one-page anchoring doc (what, why, constraints, non-goals)
2. Draft `docs/current-milestone.md` - what we're doing right now, success criteria, open questions
3. Route: what goes in Notion vs GitHub vs repo docs
4. Surface the top 3 missing assumptions before implementation starts

Keep everything ready to paste directly into files.

### Mode: existing-project

Follow `ASSISTANT.md` existing-project rules. Produce:

1. Recommend the minimum overlay: usually `START_HERE.md` + `project-spine.md` + `current-milestone.md`
2. Map existing artifacts (Notion pages, issues, PRs) into the llm-os structure - link, don't duplicate
3. Flag what's missing vs what can be deferred

### Mode: ongoing-session

Follow `ASSISTANT.md` ongoing-session rules. Read only:
1. The Notion page provided
2. `docs/START_HERE.md` (if accessible)
3. `docs/current-milestone.md` or `docs/handoffs/active-build.md`

Then:
- Pick up from the recorded next steps
- Flag any drift between Notion, repo docs, and GitHub
- Produce a scoped session plan: what we're doing today, in what order

---

## Step 5 - Session output format

End every session with a **session close block**:

```
## Session Close

**What we did:**
[2-4 lines]

**Decisions made:**
[list only real decisions, not restatements]

**Next steps:**
[concrete, owned, sequenced]

**Write-back targets:**
[which doc/Notion page/GitHub issue should be updated]
```

This block is what gets written back to Notion or the repo doc. Offer to draft
the write-back if the user wants it.

---

## Routing rules (from llm-os)

These come from the live repo but are summarised here for quick reference.
Always defer to the fetched `operating-model.md` if there's a conflict.

- **Notion** = control tower: milestones, status, owners, blockers, collaboration
- **GitHub** = canonical: code, technical docs, issues, PRs
- **Repo `docs/`** = durable implementation-ready context
- **Chat** = scratch space unless promoted into durable docs
- **OpenClaw** = exploration/expansion scratchpad; write back to repo or Notion

---

## Notes on AI coding agent usage (Claude Code & Codex CLI)

This skill works in claude.ai, Claude Code, and Codex CLI. For coding agents,
use the repo's context anchor file to point the agent at the llm-os operating
model and the project's durable docs:

| Agent | Repo context anchor file |
|-------|--------------------------|
| Claude Code | `CLAUDE.md` |
| Codex CLI | `AGENTS.md` |

Suggested snippet for either `CLAUDE.md` or `AGENTS.md`:

```markdown
## Session operating model

This project uses the llm-os operating model.
Before starting work, read: docs/START_HERE.md and docs/current-milestone.md
For full rules: https://github.com/armin-haghi/llm-os
```

When fetching llm-os files:

- Claude Code: use the Bash tool.
  ```bash
  curl -s https://raw.githubusercontent.com/armin-haghi/llm-os/main/ASSISTANT.md
  ```
- Codex CLI: use shell access with `curl`.
  ```bash
  curl -s https://raw.githubusercontent.com/armin-haghi/llm-os/main/ASSISTANT.md
  ```
- claude.ai: use `web_fetch` on the shared raw GitHub URLs, starting with
  `ASSISTANT.md`, then fetch only the additional files the current mode needs.

---

## Error handling

| Situation | Response |
|-----------|----------|
| GitHub fetch fails | Note it, proceed with summary from ASSISTANT.md content in this skill |
| Notion fetch fails | Ask user to paste the relevant content |
| Mode is ambiguous | Ask one question; don't guess |
| No next steps found in Notion | Ask: "What's the most important thing to move forward today?" |

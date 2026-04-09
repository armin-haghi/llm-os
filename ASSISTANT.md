# Assistant Entrypoint

If a user shares this document with you, use it as the operating model for the project.

This file is designed to be the only link the user needs to paste into ChatGPT or Claude.

## Your job

Help the user apply a lightweight project operating system without creating unnecessary process overhead.

Use these files as the canonical source for the system:
- `README.md` for the overall model
- `principles/operating-model.md` for source-of-truth, context budget, routing, and write-back rules
- `INSTRUCTIONS.md` for assistant behavior in this stack
- `SETUP.md` for Notion and GitHub conventions
- `TEMPLATES.md` for full document shapes
- `project-scaffold/` for starter docs

## First determine the mode

Choose one:
- `new-project`: the user is starting from scratch or near-scratch
- `existing-project`: the user wants to layer this system onto an active repo
- `ongoing-session`: the repo already uses this system and the user wants help inside it

If the mode is not obvious, ask one short question to determine it.

## Mode: new-project

Goal:
- bootstrap the minimum useful operating layer

Default output:
1. Recommend the minimum docs to create first.
2. Draft lightweight initial content for:
   - `docs/project-spine.md`
   - `docs/current-milestone.md`
   - `docs/decision-log.md` only if needed
3. Explain what belongs in Notion, GitHub, and repo docs.
4. Identify missing assumptions or open questions before implementation starts.

Rules:
- prefer the smallest sufficient set of docs
- keep outputs practical and ready to paste into files
- only use the fuller shapes from `TEMPLATES.md` when they add real value

## Mode: existing-project

Goal:
- add this system as a lightweight overlay, not a replacement

Default output:
1. Recommend the smallest initial layer to add first, usually:
   - `docs/START_HERE.md`
   - `docs/project-spine.md`
   - `docs/current-milestone.md`
2. Map existing docs, issues, PRs, and planning artifacts into this system.
3. Suggest which existing materials should be linked instead of rewritten.
4. Identify which docs are not needed yet.

Rules:
- prefer links to existing docs over duplication
- ask only for the missing facts needed to draft the first layer well
- do not add more process than the project can support

## Mode: ongoing-session

Goal:
- work inside the system already in place

Read only the smallest sufficient context in this order:
1. `docs/START_HERE.md`
2. `docs/project-spine.md`
3. one active task doc:
   - `docs/current-milestone.md`
   - `docs/handoffs/active-build.md`
   - or `docs/reviews/active-review.md`
4. only the directly relevant supporting docs

Rules:
- treat repo docs as canonical over chat history
- keep context small
- do not restate large docs unless needed
- flag drift between repo docs, Notion plans, and GitHub execution

## Shared rules

- Notion is the control tower for milestone planning, status, owners, blockers, and collaboration.
- GitHub is the canonical place for code, technical docs, issues, PRs, and code-linked execution.
- Repo docs carry durable implementation-ready context.
- Chat history is scratch space unless promoted into durable docs.
- Prefer retrieval over large pasted context.
- End substantial sessions with:
  - summary
  - decisions made or implied
  - next steps
  - recommended write-back target

## Recommended write-back targets

Update only the durable artifact that best matches the work:
- `docs/decision-log.md`
- `docs/status-update.md`
- `docs/current-milestone.md`
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- the corresponding Notion milestone page
- the relevant GitHub issue or PR

## If you are drafting docs

Keep scaffold docs lightweight by default.
Use `TEMPLATES.md` when the user wants a fuller document structure.

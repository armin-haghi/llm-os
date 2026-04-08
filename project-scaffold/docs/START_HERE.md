# Start Here

Read this file first, then choose the smallest sufficient set of documents for the task.

## Core rules
- Notion = milestone planning, status, collaboration
- GitHub repo = canonical technical truth
- GitHub issues / PRs = execution state tied to code
- OpenClaw and chat history = scratch space unless promoted into canonical docs
- Do not read the whole repo unless necessary

## Read next by tool and task

### If you are in OpenClaw exploring an idea
1. `docs/project-spine.md`
2. the relevant Notion milestone or project page summary
3. `docs/current-milestone.md` if it exists
4. stop unless more is explicitly needed

### If you are in ChatGPT reviewing or synthesizing
1. `docs/project-spine.md`
2. `docs/current-milestone.md` or the relevant Notion milestone summary
3. `docs/reviews/active-review.md` or `docs/handoffs/active-build.md`
4. only the directly relevant source docs

### If you are in Claude Code or Codex building
1. `docs/project-spine.md`
2. `docs/handoffs/active-build.md`
3. only the referenced technical docs
4. `docs/decision-log.md` if ambiguity remains
5. relevant GitHub issue or PR if available

### If you are updating project status
1. the relevant Notion milestone page
2. relevant GitHub issue / PR state
3. `docs/status-update.md`
4. `docs/current-milestone.md`

## Write-back targets
Update only the durable artifacts:
- `docs/decision-log.md`
- `docs/status-update.md`
- `docs/current-milestone.md`
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- the corresponding Notion milestone page
- the corresponding GitHub issue or PR

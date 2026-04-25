---
name: portfolio-refresh
description: Summarize the project portfolio across stages, freshness, blockers, decisions, and commercialization.
---

# Portfolio Refresh

Read:
1. one or more project overview inputs shaped like
   `templates/project-overview.yaml`, or equivalent Notion/project records with
   the same logical fields
2. any current portfolio state if it exists

For each project capture:
- project
- status
- stage
- active milestone
- freshness
- last reviewed
- owner
- blocker
- next decision
- next action
- canonical repo
- execution surface
- commercial signal

Output:
- projects by stage
- active projects
- stale projects
- blocked projects
- projects needing a human decision
- commercialization candidates
- recommended priorities

Rules:
- treat the control tower as a rollup surface, not project-level source of
  truth
- do not rewrite project milestone intent without project-level evidence
- keep parked and archived projects out of the default active priority view

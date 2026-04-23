# Templates

This directory contains the canonical operational templates used by projects
that adopt `llm-os`.

Use the smallest sufficient template:
- `templates/AGENTS.md`
- `templates/CLAUDE.md`
- `templates/project-spine.md`
- `templates/current-milestone.md`
- `templates/open-questions.md`
- `templates/session-brief.md`
- `templates/review-report.md`
- `templates/project-overview.yaml`

These files are templates for project-level artifacts that typically live under
`docs/` in a consuming project repo, except machine-readable overview/status
artifacts such as `templates/project-overview.yaml`.

Typical initialization or retrofit path for a consuming repo:
1. audit the repo's current entry surfaces and project docs
2. decide whether `docs/` is the live project-doc surface or whether a local override should be declared
3. create root `AGENTS.md` if missing
4. create only the missing canonical artifacts
5. create `project-overview.yaml`
6. fill the minimum working content before treating the repo as initialized
7. avoid parallel project-doc surfaces unless a local override makes one explicit

In a consuming repo, matching filenames between `templates/` and `docs/` are
intentional. `templates/` defines the reusable shape; `docs/` holds the live
project state.

If a repo uses `CLAUDE.md`, keep it as a thin compatibility shim derived from
`AGENTS.md`. Do not turn it into a second operating surface.

`llm-os` itself uses a repo-local override and keeps its own live project docs
under `llm-os-docs/project/`.

Do not load every template by default.
Read only the template needed for the task at hand.

# Templates

This directory contains the canonical operational templates used by projects
that adopt `llm-os`.

Use the smallest sufficient template:
- `templates/project-spine.md`
- `templates/current-milestone.md`
- `templates/open-questions.md`
- `templates/session-brief.md`
- `templates/review-report.md`
- `templates/project-overview.yaml`

These files are templates for project-level artifacts that typically live under
`docs/` in a consuming project repo, except machine-readable overview/status
artifacts such as `templates/project-overview.yaml`.

In a consuming repo, matching filenames between `templates/` and `docs/` are
intentional. `templates/` defines the reusable shape; `docs/` holds the live
project state.

`llm-os` itself uses a repo-local override and keeps its own live project docs
under `llm-os-docs/project/`.

Do not load every template by default.
Read only the template needed for the task at hand.

# Doc Surface Decision

Date: 2026-04-24
Status: active

This note defines how the `llm-os` repo should separate operational templates
from repo documentation and background material.

## Decision

Use four layers:

- `core/`: canonical operating model, agent contracts, and change policy
- `templates/`: canonical operational templates used by projects
- `docs/`: repo documentation that explains how `llm-os` works without
  overloading `README.md`
- `docs/background/`: non-canonical reference material, assessments, design
  notes, comparisons, and future-slice thinking

Agent-operable surfaces should live outside `docs/`.
In normal use, agents should act through:
- `AGENTS.md`
- `core/`
- `skills/`
- `templates/`

Use `docs/` only when deeper clarification is needed or when working on the
operating model itself.

## Read-path rule

Default read paths must not load `docs/background/` unless it is explicitly
referenced for design, comparison, or operating-model work.

In normal use:
- `README.md` is the public map
- `AGENTS.md` is the operating entrypoint
- `core/` defines the model
- `templates/` provides the reusable working artifacts
- `docs/` is supporting documentation when the entry surface is not enough or
  when operating-model clarification is needed

`docs/background/` is reference-only and excluded from default execution
context.

## Implications

- The canonical project-doc templates now live in `templates/`.
- `docs/` should not be the normal home for agent actions or default
  operational workflows.
- `docs/` should stop pretending to be both live operational artifacts and repo
  explanation at the same time.
- `docs/background/` should keep materials like:
  - assessments
  - comparisons
  - `next-slices`
  - operating-model deltas
  - other non-default design notes
- Future guidance should refer to `docs/background/`, not `/background`.

## Remaining follow-on work

1. Decide how the top-level files in `docs/` should evolve now that the
   canonical templates live in `templates/`.
2. Keep entry surfaces and read-path rules aligned with the new split.

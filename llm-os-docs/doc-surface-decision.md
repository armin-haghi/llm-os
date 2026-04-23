# Doc Surface Decision

Date: 2026-04-24
Status: active

This note defines how the `llm-os` repo should separate live project docs,
operational templates, repo-specific explanation, and background material.

## Decision

Use four layers:

- `core/`: canonical operating model, agent contracts, and change policy
- `templates/`: canonical operational templates used by projects
- `docs/`: live project-doc surface by default
- `llm-os-docs/`: llm-os-specific explanation and deeper repo documentation
- `llm-os-docs/background/`: non-canonical reference material, assessments,
  design notes, comparisons, and future-slice thinking

Agent-operable surfaces should live outside `llm-os-docs/`.
In normal use, agents should act through:
- `AGENTS.md`
- `core/`
- `skills/`
- `templates/`
- the live project-doc surface

Use `llm-os-docs/` only when deeper clarification is needed or when working on
the operating model itself.

Default assumption:
- live project docs live in `docs/`

Override rule:
- if a target repo uses a different project-doc location, that repo's local
  `AGENTS.md` must declare it explicitly
- any other target-repo overrides from llm-os defaults should also be declared
  locally
- the local repo instruction overrides the llm-os default

Typical overrides worth declaring locally:
- a non-default live project-doc location
- repo-specific write-back targets or mandatory artifacts
- extra required read-path files beyond the llm-os default
- repo-specific review, evidence, or approval requirements
- allowed or disallowed skills, tools, or execution constraints
- repo-specific entry surfaces that should be preferred over the generic
  llm-os defaults

## Read-path rule

Default read paths must not load `llm-os-docs/background/` unless it is
explicitly referenced for design, comparison, or operating-model work.

In normal use:
- `README.md` is the public map
- `AGENTS.md` is the operating entrypoint
- `core/` defines the model
- `templates/` provides the reusable working artifacts
- `docs/` is the live project-doc surface by default
- `llm-os-docs/` is supporting llm-os-specific documentation when the entry
  surface is not enough or when operating-model clarification is needed

`llm-os-docs/background/` is reference-only and excluded from default execution
context.

## Implications

- The canonical project-doc templates now live in `templates/`.
- `docs/` should be reserved for live project state unless a repo explicitly
  overrides that choice.
- `llm-os-docs/` should not be the normal home for agent actions or default
  operational workflows.
- `llm-os-docs/background/` should keep materials like:
  - assessments
  - comparisons
  - `next-slices`
  - operating-model deltas
  - other non-default design notes
- Future guidance should refer to `llm-os-docs/background/`, not `/background`.

## Remaining follow-on work

1. Keep historical background notes clearly time-scoped when they mention
   pre-cleanup structure.
2. Keep entry surfaces and read-path rules aligned with the new split.

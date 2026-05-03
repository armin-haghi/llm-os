---
name: project-audit
description: Audit one project for LLM-OS readiness, gaps, compatibility, and source-of-truth drift.
---

# Project Audit

Use this skill when the human asks whether a project is ready for `llm-os`
orchestration or asks to find `llm-os` gaps in a project.

Trigger phrases:

- "Audit <project> for LLM-OS gaps"
- "Is <project> ready for LLM-OS?"
- "Check whether <project> can run through the Agent Run Queue"
- "What is missing for <project> to use llm-os?"

## Read

Use:

- `orchestration/prompts/project-audit.md`

The audit should load only the surfaces needed by the prompt:

1. Project Control Tower record
2. Agent Run Queue records for the project
3. project repo `AGENTS.md` or equivalent entrypoint
4. project repo `project-overview.yaml`
5. project current milestone and session brief
6. canonical `llm-os` `llm-os-docs/version-log.md`
7. canonical `llm-os` `llm-os-docs/consistency-check.md`

## Output

Return:

- overall readiness classification
- check table with status, finding, and fix
- compact YAML-style summary
- recommended next action
- whether to create or update an Agent Run Queue item

## Rules

- This is a readiness and conformance audit, not a product critique.
- Do not modify project files by default.
- Prefer one bounded migration or sync run over many small tasks.
- Mark projects as `blocked` when structure is good but a named human input is
  required.
- Mark projects as `needs-migration` when they are structurally usable but behind
  the current `llm-os` standard.
- Do not recommend or create GitHub issues by default. Use issues only when the
  project already uses them as its execution surface or the human explicitly
  asks for issue-based tracking.

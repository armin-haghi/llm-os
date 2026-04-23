# CLAUDE.md

This file is a compatibility shim for Claude.

`AGENTS.md` is the source of truth.
If this file conflicts with `AGENTS.md`, follow `AGENTS.md`.

## Read first
1. `AGENTS.md`
2. the repo's live project-doc surface
3. only then directly relevant supporting docs if needed

## Critical rule

Keep things minimal.

Do not:
- invent extra process layers
- propose new control files when `AGENTS.md` already covers the need
- treat missing `CLAUDE.md` as a major gap if `AGENTS.md` exists
- create parallel sources of truth
- broaden scope just because a tool-specific harness could exist

## What to do instead

- use `AGENTS.md` as the operating entrypoint
- follow the repo's declared live project-doc surface
- fall back to canonical `llm-os` defaults only when the local repo surface is missing or ambiguous
- prefer the smallest sufficient change and the smallest sufficient context

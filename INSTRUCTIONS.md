# Operating Model Instructions

Instructions for each role and tool in the stack.

## OpenClaw — Exploration

Use this session as working space, not canonical memory.

OpenClaw is primarily for:
- Idea expansion
- Branching alternatives
- Rough planning
- Turning vague concepts into candidate milestone plans or handoffs

### Rules
1. Work against the current milestone or question only.
2. Prefer structured outputs over long freeform transcripts.
3. Do not assume old session content is canonical unless it appears in repo docs or Notion.
4. Stay one level above implementation unless explicitly asked to produce a builder handoff.
5. End each substantial session with:
   - summary
   - key options or decisions
   - unresolved questions
   - recommended write-back target
6. If a builder will consume the output, shape it into `docs/handoffs/active-build.md`.
7. If the output is for critique, shape it into `docs/reviews/active-review.md`.

---

## ChatGPT — Synthesis & Review

Primary role in this stack:
- Synthesize messy material into clear artifacts
- Review plans before build
- Compare options and tradeoffs
- Reduce token load by choosing the smallest useful context

### Reading order
1. `docs/START_HERE.md`
2. `docs/project-spine.md`
3. The active milestone, review, or handoff doc
4. At most 2 to 3 directly relevant supporting docs

### Output shape
Treat `docs/decision-log.md` as authoritative over chat history.
Do not restate large documents unless asked.
When possible, turn output into one of:
- A review artifact
- A cleaned-up handoff
- A decision summary
- A status update

### End with
- Summary
- Decisions
- Next steps
- Recommended write-back target

Flag drift between Notion plans, repo docs, and GitHub execution.

---

## Claude Code / Codex — Build

You are acting as a builder inside a stack that uses Notion for milestone planning and GitHub for technical truth.

### Primary sources (in order)
1. `docs/START_HERE.md`
2. `docs/project-spine.md`
3. `docs/handoffs/active-build.md`
4. Only the referenced technical docs needed for implementation
5. `docs/decision-log.md` if an implementation choice is ambiguous

### Builder rules
- Prefer explicit file-level changes
- Prefer acceptance criteria and testable outputs
- Do not infer product decisions that are not documented in canonical docs
- If the handoff is incomplete, state what is missing instead of inventing it silently
- Map implementation work back to the relevant GitHub issue or PR when possible

### End with
- Implementation summary
- Changed files or intended changes
- Unresolved questions
- Recommended write-back target

---

## Roles — Lightweight task modes

### Role: Explorer
Use OpenClaw-style exploration: generate options, unknowns, risks, alternatives, and tradeoffs.
Do not prematurely commit to implementation.
Promote only stable findings into Notion or canonical repo docs.

### Role: Builder
Work from the active handoff and technical repo docs.
Prefer explicit file changes, constraints, acceptance criteria, and GitHub-linked execution.
Do not invent missing product decisions.

### Role: Reviewer
Use ChatGPT-style review: critique assumptions, identify gaps, surface risks, simplify plans, and strengthen handoffs.
Structure feedback against the review template.

### Role: Tracker
Update milestone status, blockers, dependencies, and next decisions in Notion.
Update implementation-linked execution in GitHub issues and PRs.
Do not modify technical truth unless reflecting a confirmed decision.

---

## Stack context

This stack-specific workflow:
- **Notion** = milestone planning, status, collaboration
- **GitHub repo** = canonical technical truth
- **GitHub issues / PRs** = execution state
- **OpenClaw** = exploration scratchpad
- **Operate from canonical docs**, not transcript memory

Canonical sources:
1. `docs/project-spine.md` and `docs/decision-log.md` over chat history
2. Notion for milestone planning and status
3. GitHub for technical truth, issues, pull requests, and code-linked execution
4. OpenClaw sessions and chat transcripts are scratch space unless promoted

Do not ingest or restate large documents unless necessary. Prefer the smallest sufficient set of documents.

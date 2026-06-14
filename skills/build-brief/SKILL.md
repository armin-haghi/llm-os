# Build Brief Skill

Use this skill when the human wants to turn a problem, product idea, chat thread, Notion note, or milestone slice into something a coding agent can build.

The output should use `templates/build-brief.md` and produce two parts:

1. Product Build Brief — what should be built and why.
2. Agent Run Packet — what the coding agent should read, change, test, and write back.

## When to use

Use when:

- the human describes a business need or product problem
- the next step is likely implementation
- the current context is too vague for a coding agent
- a handoff is needed for ChatGPT, Claude, Codex, Claude Code, or another coding agent

Do not use for:

- tiny code edits
- pure debugging
- broad strategy work
- unresolved product direction
- work that needs a human decision before shaping

## Inputs

Read the smallest useful context.

Prefer:

1. the human's request
2. `AGENTS.md`
3. `project-overview.yaml`
4. `docs/current-milestone.md`
5. `docs/session-brief.md`
6. relevant architecture, schema, API, or design docs only when directly needed

If the repo uses a local project-doc override, follow the local `AGENTS.md`.

## Procedure

1. Identify the business need and desired product outcome.
2. Convert the workflow into a user journey with happy path and error paths.
3. Define scope and non-goals.
4. Write requirements with observable done checks.
5. Name the components, data shapes, and tech decisions needed for the build.
6. Fill the Agent Run Packet: goal, read path, likely files, permissions, environment, verification, and write-back targets.
7. Use default assumptions for minor gaps.
8. Surface only decisions that require the human.

## Output location

Default output:

- `docs/handoffs/active-build.md`

Use a named file only when multiple briefs need to be preserved:

- `docs/build-briefs/[slug].md`

## Rules

- Keep the brief bounded to one milestone slice or one agent run.
- Do not create a second project plan.
- Do not turn the brief into a backlog.
- Separate product intent from implementation instructions.
- Keep `llm-os` as operating methodology, not product runtime architecture.
- Make done checks observable.
- Include data shapes when data crosses a boundary.
- Include files likely touched when known.
- Include verification commands when known.
- Include write-back targets.

## Human escalation

Ask the human only when:

- the goal is ambiguous
- scope tradeoff is required
- an architecture choice has meaningful consequences
- credentials, secrets, or paid services are needed
- risk acceptance is required
- repo docs and Notion disagree

Otherwise, choose a reasonable default and mark it as an assumption.

## Closeout

End with:

- brief path created or updated
- assumptions made
- human decisions needed, if any
- recommended next agent run

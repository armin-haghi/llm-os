# Notion and GitHub Setup

Recommended conventions and structures for integrating with Notion and GitHub.

---

## Notion Setup

Use Notion as the milestone and collaboration layer.

### Recommended databases

#### Projects
Fields:
- Name
- Status
- Owner
- Objective
- Repo link
- Project spine link
- Current milestone
- Last update

#### Milestones
Fields:
- Milestone name
- Project
- Status
- Goal
- Owner
- Target date
- Depends on
- Risks
- Open questions
- Build handoff link
- Review doc link
- GitHub issue / project link
- Last update

#### Decision summaries
Fields:
- Decision
- Project
- Date
- Status
- Link to repo decision log
- Impacted milestone

### Recommended page structure for each milestone
- Objective
- Scope
- Non-goals
- Success criteria
- Risks
- Dependencies
- Comments / reviewer input
- Latest summary
- Linked repo docs
- Linked GitHub issues / PRs

---

## GitHub Setup

Use GitHub for technical truth and code-linked execution.

### Issues

Each implementation issue should link to:
- Current milestone
- Active build handoff
- Relevant decision(s)

Suggested issue sections:
- Objective
- Scope
- Acceptance criteria
- Dependencies
- Linked docs

### Pull requests

Suggested PR sections:
- Summary
- Linked issue
- Decisions reflected
- Docs updated
- Remaining follow-ups

### Doc linkage

Each active milestone should ideally link to:
- Notion milestone page
- `docs/current-milestone.md`
- `docs/handoffs/active-build.md`
- Relevant issue / PR

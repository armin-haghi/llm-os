# llm-os Alignment Assessment

Historical note: this assessment was written before later cleanup passes. It
may reference issues that have since been resolved, and file paths inside it may
reflect older repo structure.

**Date:** 2026-04-24  
**Scope:** Current state vs. documented vision and next-slices roadmap  
**Context:** Pre-first-project assessment; framework is in "now/next" transition phase

---

## Executive Summary

`llm-os` has a coherent and well-articulated vision (an operating standard for agent-driven product work) with solid conceptual foundations. The **core model is sound**, but there are **meaningful gaps between designed concepts and integrated implementation**. Several items marked "now" in next-slices are unfinished, and recent operating-model updates (routing layer, operating-model-update mode, read-path rules) are documented but not fully integrated into entry points and skills.

The framework is ready for internal refinement but not yet ready for first-project onboarding without addressing integration gaps.

---

## Strengths

### Conceptual Clarity
- **Stage/milestone/task distinction** is clean and well-motivated
- **Narrow agent contracts over broad roles** is a sound design direction
- **Canonical durable docs** (project spine, milestone, open questions, session brief, review report) create genuine memory without chat drift
- **Explicit human as decision endpoint** is honest about what agents can't do

### Boundary Discipline
- **Change policy** is clear (experiment → candidate → standard)
- **Non-goals** are explicit (not a company OS, not agile, not backlog-heavy)
- **Reference framework comparison** shows careful judgment about borrowing selectively from BMAD, gstack, HookDevAgents, etc.
- **Lifecycle framing** (Think→Plan→Build→Review→Ship→Reflect) is crisp and properly documented

### Documentation Quality
- **Operating model docs** (core/) are thorough and well-structured
- **Agent contracts** are specific with clear inputs, outputs, escalation conditions
- **Background materials** (next-slices, ops-model-delta, framework-comparison) show design thinking
- **Templates** provide good structure for project docs

---

## Critical Gaps (Things Marked "Now" but Not Implemented)

These are roadmap items in `next-slices.md` with `status: now`, meaning they should be complete before first-project use. They are not yet implemented:

### 1. Platform Playbook
- **What:** `core/platform-playbook.md`
- **Why it matters:** Provides single practical guide across tools without bloating README
- **Status:** Not found
- **Impact:** New users will hit AGENTS.md without knowing tool conventions, write-back expectations, or escalation signals
- **Trigger (from next-slices):** "before onboarding first real project"

### 2. Cheap OpenClaw Input Skill
- **What:** `capture-human-input` skill
- **Why it matters:** Enables lightweight conversational input without pulling full execution context
- **Status:** Not found
- **Impact:** When running multiple projects, humans have no lightweight way to surface decisions without disrupting work sessions
- **Trigger:** "before using OpenClaw as primary control surface"

### 3. Human-Topic Surfacing Skill
- **What:** `surface-human-topics` skill (or equivalent)
- **Why it matters:** Ensures decision-worthy and uncertain items bubble up automatically
- **Status:** Not found
- **Impact:** Without this, human decisions pile up in discussion rather than being captured as explicit open questions
- **Trigger:** "before running multiple active projects in parallel"
- **Note:** Related but not the same as the `surface-uncertainty` agent contract (which is human-interface, not agent-automated)

### 4. Minimum Project Overview Input Format
- **What:** Defined schema for `project`, `stage`, `active milestone`, `freshness`, `blocker`, `next action`, `commercial signal`
- **Why it matters:** Enables reliable project overview refresh and portfolio tracking
- **Status:** Fields are named in next-slices but no template or schema exists
- **Impact:** `portfolio-refresh` contract and `portfolio-refresh` skill lack a structured input format
- **Trigger:** "before running portfolio refresh in practice"

---

## Integration Inconsistencies

### 1. Operating-Model-Update Mode Not Integrated

**Design:** Documented in `ops-model-delta.md` and `next-slices.md`
- Purpose: isolate changes to the operating model itself (AGENTS.md, ASSISTANT.md, templates, workflow rules)
- Trigger: any change to core files
- Required elements: reason, impact, affected files, followed by consistency check

**Current state:**
- ✓ Designed in detail in `ops-model-delta.md`
- ✓ Listed as "now" in `next-slices.md`
- ✗ **NOT listed in AGENTS.md modes** (only lists `new-project`, `existing-project`, `ongoing-session`)
- ✗ **NOT listed in `skills/llm-os-session/SKILL.md` modes**
- ✗ No consistency-check template or guidance

**Impact:** If someone needs to change the operating model, they won't know this mode exists or how to invoke it. Changes to core files could propagate without consistency checks.

**Fix needed:**
1. Add `operating-model-update` to AGENTS.md mode list with trigger and rules
2. Update `llm-os-session/SKILL.md` to include the mode
3. Create a consistency-check template or guidance

---

### 2. Read-Path Rule Not Enforced in Entry Points

**Design:** Documented in `ops-model-delta.md` Δ3 and Δ6
- `/background` docs MUST NOT be loaded unless explicitly referenced
- Default read path: AGENTS.md → active milestone → task/plan → decisions → only then other docs

**Current state:**
- ✓ Designed and documented in `ops-model-delta.md`
- ✓ Listed as "now" item: "Enforce default read path"
- ✗ **NOT mentioned in AGENTS.md**
- ✗ **NOT mentioned in `llm-os-session/SKILL.md`**
- ✗ No enforcement mechanism

**Impact:** A new user reading AGENTS.md will load `docs/background/` by default, defeating the "minimal context" principle. Background docs (next-slices, ops-model-delta, etc.) will pollute the default session context.

**Fix needed:**
1. Add explicit read-path guidance to AGENTS.md: "Do not load `/background` docs unless explicitly referenced"
2. Update each mode description in AGENTS.md to show the minimal read order
3. Add to `llm-os-session/SKILL.md`

---

### 3. Routing Layer Documented but Not Applied per Mode

**Design:** Documented in `ops-model-delta.md` Δ1 and Δ5
```
Think → Plan → Build → Review → Ship → Reflect
```

Per-mode routing guidance:
- `ongoing-session`: Think → Build
- `execution`: Build → Review → Ship
- `review`: Review only
- `existing-project`: Think → Plan
- `new-project`: Think → Plan

**Current state:**
- ✓ Documented in `ops-model-delta.md`
- ✓ Listed as "now" item: "Add routing layer"
- ✗ **NOT shown in AGENTS.md**
- ✗ **NOT shown in skill SKILL.md files**
- ✗ No guidance on which steps are optional per mode

**Impact:** A practitioner reading AGENTS.md won't know whether a `ongoing-session` skips Planning, whether Review is mandatory, or whether Reflect is always implicit. This creates ambiguity about execution flow.

**Fix needed:**
1. Add routing table to AGENTS.md showing lifecycle steps per mode
2. Update mode descriptions to reference the routing table
3. Document whether each step is required, optional, or implicit

---

### 4. Templates vs. Example Project Docs

**Current state:**
- `docs/project-spine.md` — contains template structure, not a filled-in spine
- `docs/current-milestone.md` — contains template structure, not a filled-in milestone
- `docs/open-questions.md` — contains template structure only
- `docs/session-brief.md` — contains template structure only
- `docs/review-report.md` — contains template structure only

**Issue:**
This is ambiguous. If llm-os is a pure framework, then:
- ✓ These templates are correct in `/docs/`
- ✗ But a new user has no example of what a "correct" filled-in spine looks like
- ✗ No bootstrap example to work from

If llm-os is also a "project" (meta-level), then:
- ✗ These should be filled in with actual project spine, milestone, etc.
- ✗ Currently they're templates, not content

**Fix needed:**
One of two approaches:
1. **Clarify intent:** Add a note to `/docs/` explaining these are templates and point to `/core/templates/` as the canonical template location
2. **Provide example:** Create a minimal reference project (real or synthetic) as a worked example of filled-in docs, either in `/docs/examples/` or in a separate reference project

---

### 5. Agent Contracts Without Corresponding Skills

**Defined contracts:**
- `project-refresh` — ✓ has skill
- `review-gate` — ✓ has skill
- `portfolio-refresh` — ✓ has skill
- `surface-uncertainty` — ✗ no skill found
- `critique-solution` — ✗ no skill found
- `package-decision` — ✗ no skill found

**Analysis:**
The human-interface contracts (`surface-uncertainty`, `critique-solution`, `package-decision`) may intentionally not have skills (they're human-led). But this isn't documented in AGENTS.md or `agent-contracts.md`.

**Impact:** Unclear whether these contracts are meant to be:
- Always human-led (no skill needed)
- Future skills to be built
- Integrated into other workflows

**Fix needed:**
Add a note to `agent-contracts.md` clarifying the relationship between contracts and skills, and explaining why some contracts don't have corresponding skills.

---

## Friction Points for First-Time Use

### 1. No Bootstrapping Example
When a new user opens AGENTS.md, they immediately face: "Determine one mode before proceeding." For someone new to the system, this is a cliff. The recommendation to "ask one short clarification question" is good, but there's no worked example of what that conversation looks like.

**Fix:** Add a "Getting started" section to AGENTS.md with a minimal example: "If you're starting a new project, the first session should read [these docs] and ask [this question]."

### 2. Canonical Links Are Self-Referential
The project-spine template mentions "Canonical links: Project repo, deployed surface, spec, dashboards, data sources, or customer notes." For llm-os itself, what should these point to? The template assumes an external product, not the OS itself.

**Fix:** Add a note in the template or in project-spine.md explaining how canonical links work for framework/OS-level projects.

### 3. No ASSISTANT.md Equivalent
The operating-model.md mentions "Entry points: interfaces only, not source of truth" and "Notion: portfolio state, ownership, blockers, human decisions." But there's no mention of what an ASSISTANT.md (or Claude Code config) should look like in this context.

**Fix:** Create a minimal guide or example of how llm-os should be configured in various entry points (Claude Code, Notion, OpenClaw, etc.).

---

## Consistency Check Against Change Policy

The `change-policy.md` states:

> "When a core concept changes, update impacted layers together so entrypoints, templates, and skills do not drift."

**Impacted layers:**
- Core concepts: operating-model.md
- Entry points: AGENTS.md, skills/*/SKILL.md
- Templates: core/templates/minimal.md
- Documentation: agent-contracts.md, operating-model.md

**Current drift:**
- `operating-model-update` mode: designed but not in AGENTS.md or skills
- Read-path rules: designed but not in AGENTS.md or skills
- Routing layer: designed but not mapped per-mode in AGENTS.md or skills
- Skills: only 4 of 6 contracts have corresponding skills, relationship unclear

**Recommendation:** Before considering this "ready," run a consistency check:
1. Update AGENTS.md to reflect all recent design changes (modes, read path, routing)
2. Update all skill SKILL.md files to match AGENTS.md
3. Verify templates match the updated mode descriptions
4. Confirm no drift between agent-contracts.md and implemented skills

---

## Status of "Now" Items from Next-Slices

| Item | Status | Blocker | Notes |
|------|--------|---------|-------|
| Replace roles with agent contracts | ✓ Done | None | `agent-contracts.md` exists and is solid |
| Cheap OpenClaw input skill | ✗ Not started | Design | Marked "now"; needed before multi-project use |
| Human-topic surfacing skill | ✗ Not started | Design | Marked "now"; complements surface-uncertainty contract |
| Platform playbook | ✗ Not started | Design | Marked "now"; critical for onboarding |
| Project overview input format | ✗ Not started | Design | Marked "now"; schema not defined |
| Add routing layer | ✓ Designed, partial | Integration | In `ops-model-delta.md`; not in AGENTS.md |
| Add operating-model-update mode | ✓ Designed, partial | Integration | In `ops-model-delta.md`; not in AGENTS.md or skills |
| Enforce default read path | ✓ Designed, partial | Integration | In `ops-model-delta.md`; not in AGENTS.md or skills |
| Add lightweight guardrails | ✓ Designed | Verification | Mentioned in ops-model-delta; unclear if enforced |

**Summary:** Design work is done on most items, but integration into AGENTS.md and skills is incomplete. Integration gaps represent a consistency violation per change-policy.

---

## Recommended Sequencing

To prepare llm-os for first-project onboarding:

### Phase 1: Integration (Sync Design with Entry Points)
1. Update AGENTS.md with `operating-model-update` mode, read-path rule, routing table
2. Update all skill SKILL.md files to match updated AGENTS.md
3. Verify change-policy consistency across core/entry-points/skills
4. Add explicit clarification guidance to AGENTS.md modes section

### Phase 2: Scaffolding (Fill "Now" Gaps)
1. Create `core/platform-playbook.md`
2. Define project-overview input schema and template
3. Design `capture-human-input` skill (or equivalent lightweight entry point)
4. Design `surface-human-topics` skill

### Phase 3: Onboarding Readiness
1. Create getting-started example or minimal reference project
2. Add ASSISTANT.md equivalents or tool-specific config guidance
3. Final consistency check (all layers aligned)
4. Test with first real project

---

## What's Working Well

- **Operating model philosophy** is sound and well-motivated
- **Canonical project docs** will prevent drift if write-back discipline is enforced
- **Escalation rules** are clear enough to be followable
- **Boundary discipline** (what llm-os is and isn't) is mature
- **"Now" vs "next" vs "later" stratification** shows good prioritization judgment
- **Framework comparison** is honest and avoids over-engineering

---

## Conclusion

`llm-os` is **well-designed but partially integrated**. The conceptual work is solid; the main work remaining is connecting designed concepts back to entry points and filling in scaffolding items marked "now."

This is not an architectural problem — it's a consistency and completeness problem. The fixes are straightforward (update AGENTS.md, sync skills, fill platform playbook) but necessary before the first real project can depend on the system with confidence.

**Recommended:** Complete Phase 1 (integration) before onboarding a project, then Phase 2 (scaffolding) in parallel with early project work.

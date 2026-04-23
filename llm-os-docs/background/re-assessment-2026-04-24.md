# Re-Assessment: Post-Cleanup Alignment

**Date:** 2026-04-24  
**Context:** Assessment after major structural changes addressing previous alignment gaps  
**Baseline:** Initial alignment-assessment.md + repo-alignment-assessment.md

---

## Executive Summary

The changes since the last assessment have been **significant and well-executed**. The repo has moved from "well-designed but partially integrated" to "materially more coherent with clearly bounded remaining risks."

**Status:** Conditional go for real-project validation.

The core operating surface is now internally consistent. The main remaining work is validation (real-project proof) rather than design or integration. Historical background notes are the only significant ambiguity, and they're already scoped as a follow-on, not a blocker.

---

## What Changed: Gap Resolution

### 1. ✅ Doc-Surface Boundaries (Was Open Question #1)
**Previous state:** Ambiguous — unclear whether `/background` was truly non-default or if templates/project-docs should be filled in.

**Current state:**
- `doc-surface-decision.md` explicitly defines layers:
  - `core/`: operating model, contracts, playbook, decisions
  - `templates/`: reusable canonical templates
  - `docs/`: live project surface for consuming repos
  - `llm-os-docs/project/`: live project surface for llm-os itself (explicit override)
  - `llm-os-docs/`: explanatory docs for llm-os work
  - `llm-os-docs/background/`: non-default reference material (assessments, comparisons, design notes)
- Rule is explicit: background docs excluded from default execution context
- `AGENTS.md` enforces this rule: "do not load by default... unless explicitly referenced"

**Status:** ✓ Resolved. Clear, documented, enforced in entry points.

---

### 2. ✅ Self-Hosted Project Docs (Was Open Question #2)
**Previous state:** Templates in `/docs/` but unclear if llm-os should be a self-hosted example.

**Current state:**
- llm-os now self-hosts its project docs in `llm-os-docs/project/`:
  - `project-spine.md` — filled in with what, why, who, constraints, success criteria
  - `current-milestone.md` — active milestone with clear scope, acceptance criteria, dependencies, blockers
  - `open-questions.md` — two explicit questions with owners and decide-by dates
  - `session-brief.md` — current working context and risks
  - `review-report.md` — consistency pass showing "conditional pass" with known risks
- `templates/` remains canonical reusable template layer for consuming repos
- Clear separation: `docs/` is default for consumers; `llm-os-docs/project/` is llm-os override

**Status:** ✓ Resolved. Proves the loop works end-to-end; provides a reference example.

---

### 3. ✅ Routing Integration (Was Gap #2 & #3)
**Previous state:** Routing designed in ops-model-delta but not shown per-mode in AGENTS.md.

**Current state:**
- AGENTS.md now shows the routing pattern explicitly:
  ```
  Think -> Plan -> Build -> Review -> Ship -> Reflect
  ```
  Applied per-mode:
  - `new-project`: Think → Plan
  - `existing-project`: Think → Plan (+ execute against surface)
  - `ongoing-session`: Think → Build (with Review/Ship/Reflect only as needed)
  - `operating-model-update`: Think → Plan → Build → Review (+ consistency check)

**Status:** ✓ Resolved. Clear, integrated, per-mode guidance in entry point.

---

### 4. ✅ Operating-Model-Update Mode (Was Gap #1)
**Previous state:** Designed in ops-model-delta but not in AGENTS.md or skills.

**Current state:**
- Listed in AGENTS.md as a mode with explicit rule: "followed by a consistency check across entry surfaces"
- Session-brief notes this as a valid session contract
- Clear trigger: when core files or operating surfaces are being changed

**Status:** ✓ Resolved. Integrated into mode list and entry points.

---

### 5. ✅ Missing Core Scaffolding (Was Phase 2 Gap)
**Previous state:** Platform playbook, external-skills boundary, freshness model, decisions log were listed as "now" items but not found.

**Current state:**
- ✓ `core/platform-playbook.md` — defines practical operating guidance across entry points
- ✓ `core/external-skills.md` — defines boundary between core (operating model) and external (capability-specific)
- ✓ `core/freshness-model.md` — defines stale-context rules and refresh triggers
- ✓ `core/decisions.md` — log of load-bearing operating-model decisions
- ✓ Lightweight human-input skills referenced in session-brief (though implementation status unclear)

**Status:** ✓ Mostly resolved. Core playbooks exist; human-interface skill implementations may still be partial.

---

### 6. ✅ ASSISTANT.md Equivalent (Was Open Question #3)
**Previous state:** Unclear what this should be or whether it was needed.

**Current state:**
- Not created as a separate file, but the need is addressed through:
  - `AGENTS.md` as the primary entry point (functions like ASSISTANT.md)
  - `core/platform-playbook.md` defines tool-agnostic practical operating guidance
  - Tool-specific configs can point to AGENTS.md and read context from there
  - `doc-surface-decision.md` addresses multi-tool entry-point consistency

**Status:** ✓ Resolved. Need is met through existing entry points without creating a redundant file.

---

## Remaining Risks & Ambiguities

### Risk 1: Historical Background Notes Still Stale
**What:** Older assessment and delta notes in `llm-os-docs/background/` still reference pre-cleanup structure.

**Examples:**
- `alignment-assessment.md` (my first doc) references gaps that have now been resolved but doesn't know about the new structure
- `assessment-comparison.md` may reference outdated state
- `repo-alignment-assessment.md` was written before the cleanup and talks about "templates vs self-hosted" as a gap

**Impact:** Low. These are explicitly in `llm-os-docs/background/` (non-default context), but a reader could be confused if they load them during decision-making.

**Current stance (from review-report):** Leave them marked as historical; move to real-project validation rather than rewriting all historical docs immediately.

**Recommendation:** Add a time-scoped header to historical background notes (e.g., "Pre-cleanup structure: This doc reflects state before 2026-04-24 reorganization. See llm-os-docs/doc-surface-decision.md for current structure.") instead of full rewrite.

---

### Risk 2: Real-Project Validation Not Yet Done
**What:** The current operating surface is coherent, but it hasn't been tested end-to-end on a real project outside llm-os itself.

**Current state:** llm-os self-hosts, which provides proof of concept. But a real consuming project might hit gaps:
- Override behavior (repo-local AGENTS.md declaring non-default `docs/` location) has not been exercised
- Edge cases in multi-tool entry points may not be obvious until used
- Platform playbook assumptions may not hold in all contexts

**Impact:** Medium. The risks are known and scoped. This is exactly what the next milestone (real-project validation) is for.

**Status:** Expected and accepted. Review-report calls this out explicitly.

---

### Risk 3: Human-Interface Skills Status Unclear
**What:** Session-brief mentions "lightweight human-input skills" as part of the current state, but skill implementation status is unclear.

**Current state:**
- Contracts are defined: `surface-uncertainty`, `critique-solution`, `package-decision`
- `capture-human-input` and `surface-human-topics` are in next-slices
- But are there actual skill implementations? Or just contracts?

**Impact:** Low if this is intentional (contracts only, no skills yet). Medium if skills are expected to exist.

**Recommendation:** Clarify in the session-brief or current-milestone whether human-interface skills are implemented as skills, or if they remain human-driven contracts with just contract definitions.

---

### Risk 4: Model-Rightsizing Not Yet Integrated
**What:** `llm-os-docs/background/model-rightsizing.md` introduces a new concept (routing tasks to appropriate model size with safe escalation) but it's not yet integrated into the operating model or agent contracts.

**Current state:** Documented as a requirement/need, not yet part of core or skills.

**Impact:** Low. It's a future consideration properly placed in background. But if this is a "now" priority, it should be moved into active work.

**Recommendation:** Clarify whether model-rightsizing is a near-term need (should move to current-milestone or next-slices) or a future refinement (stays in background).

---

## What Is Genuinely Ready

### ✓ Operating Model Core
- Clear concepts: stages, milestones, tasks, lanes, agent contracts, human decision endpoint
- Well-motivated and consistent

### ✓ Entry Point Surface
- AGENTS.md is now comprehensive: modes, routing per-mode, read paths, required behavior
- README.md exists for public orientation
- Platform playbook provides practical guidance

### ✓ Boundary Documentation
- doc-surface-decision.md defines layer separation
- external-skills.md defines capability boundary
- change-policy.md is clear
- freshness-model.md defines staleness rules

### ✓ Self-Hosted Example
- llm-os-docs/project/ proves the loop works
- Project spine, milestone, decisions are filled in
- Shows consumers what a "correct" project spine looks like

### ✓ Reusable Template Layer
- templates/ is now clearly canonical
- Consuming repos have a reference to work from
- Template structure matches actual project doc patterns

### ✓ Decision Log
- core/decisions.md captures load-bearing decisions
- Makes it clear what's been decided vs. what's still open

---

## What Still Needs Work

### Phase 2 Scaffolding (Mostly In Background But Worth Noting)
From next-slices "now" items, still incomplete:
- [ ] Cheap OpenClaw input skill (capture-human-input)
- [ ] Human-topic surfacing skill (surface-human-topics)
- [ ] Project-overview input format (for portfolio refresh)

**Status:** Designed/documented, not yet fully implemented. These are "nice to have" before multi-project parallelization, but not blockers for first real project.

---

### Historical Doc Cleanup
- Timeline notes should be added to background docs explaining when structure changed
- Some older analysis docs could have "pre-cleanup" headers

**Status:** Acknowledged in review-report and current-milestone open questions. Intentionally deferred.

---

## How This Compares to Earlier Gaps

| Earlier Gap | Status | Evidence |
|-------------|--------|----------|
| No single read path | ✓ Resolved | AGENTS.md shows clear path per mode; platform-playbook reinforces |
| Mode/routing mismatch | ✓ Resolved | AGENTS.md shows routing per mode explicitly |
| Entry surface incomplete | ✓ Resolved | AGENTS.md, platform-playbook, skills all aligned |
| Background boundaries loose | ✓ Resolved | doc-surface-decision.md + AGENTS.md enforcement |
| Template vs self-hosted ambiguity | ✓ Resolved | templates/ for canonical, llm-os-docs/project/ for self-hosted |
| Human-interface contracts ahead of skills | ⚠ Partial | Contracts defined; skill implementation status unclear |
| Operating-model-update not integrated | ✓ Resolved | In AGENTS.md as a mode with consistency-check requirement |
| Platform playbook missing | ✓ Resolved | core/platform-playbook.md exists |
| ASSISTANT.md unclear | ✓ Resolved | Need addressed through AGENTS.md + platform-playbook |
| Project overview schema missing | ⚠ Partial | Not yet seen; needs validation or clarification |

---

## Next Steps to Proceed

### Decision Point #1: Handle Historical Docs (Choose One)
**Option A (Recommended):** Add time-scoped headers to pre-cleanup background docs (quick, non-blocking)
- Add header: "Written before 2026-04-24 cleanup. See llm-os-docs/doc-surface-decision.md for current structure."
- Takes ~30 min
- Unblocks real-project validation without rewriting

**Option B:** Full historical reconciliation (comprehensive but heavier)
- Rewrite docs to reference current structure
- Takes ~2-3 sessions
- Can be done in parallel with real-project setup

**Recommendation:** Choose A. Historical clarity can improve in parallel with validation work.

---

### Decision Point #2: Prioritize Next Milestone
**Option A (Recommended per review-report):** Real-project validation
- Use this surface on an actual consuming project
- Discover edge cases, integration issues, missing patterns
- Next milestone: "Run first real project end-to-end on llm-os surface"

**Option B:** Fill Phase 2 Scaffolding First
- Build OpenClaw input skill, human-topic surfacing
- Define project-overview schema
- Test multi-project parallelization

**Recommendation:** Choose A. Real-project validation will drive what scaffolding actually gets built. Designing scaffolding without validation risk is premature.

---

### Action Sequence

1. **Now:** 
   - Choose Decision Point #1 approach (time-scoped headers vs full rewrite) 
   - Define target consuming project for validation

2. **Create next milestone:**
   - Milestone: "First real project validation on current operating surface"
   - Scope: onboard a real project, run 1-2 active sessions, collect gaps/surprises
   - Success criteria: project runs successfully without discovering design-level gaps (implementation gaps are OK)

3. **During validation:**
   - Discover actual gaps vs theoretical ones
   - Collect patterns that belong in the playbook
   - Build Phase 2 scaffolding driven by real needs, not speculation

4. **After validation:**
   - Update core docs with validated patterns
   - Then decide: expand operating model or scale what exists

---

## Assessment Verdict

**Alignment Status:** ✅ **Ready for conditional go**

The operating model is coherent, the integration is complete, and the entry surfaces are consistent. Self-hosting proves the loop works. Historical ambiguity is scoped and non-blocking.

**Confidence Level:** High for internal coherence; moderate for external validation.

**Recommended Next Move:** Real-project validation, not more theory.

The repo is no longer asking "is the model right?" It's ready to ask "does this model work in practice?" That's a different, more valuable question.

---

## Appendix: Files Added/Changed Since Last Assessment

**Created:**
- `llm-os-docs/` (new directory structure)
- `llm-os-docs/project/` (live project docs)
- `llm-os-docs/doc-surface-decision.md` (layer definition)
- `core/platform-playbook.md` (practical guidance)
- `core/external-skills.md` (capability boundary)
- `core/freshness-model.md` (staleness rules)
- `core/decisions.md` (decision log)
- `llm-os-docs/background/model-rightsizing.md` (model-routing requirement)

**Updated:**
- `AGENTS.md` (routing table, operating-model-update mode, read-path rules, explicit layer references)
- `core/agent-contracts.md` (minor updates for consistency)

**Moved/Reorganized:**
- Historical assessment docs moved to `llm-os-docs/background/`
- Docs structure split: consuming-repo convention in `templates/` and `docs/`, llm-os override in `llm-os-docs/project/`

---

**Prepared:** Claude Code session 2026-04-24  
**Reviewer context:** Post-cleanup coherence assessment

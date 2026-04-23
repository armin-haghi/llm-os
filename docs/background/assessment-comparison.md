# Assessment Comparison & Next Steps

**Date:** 2026-04-24  
**Documents compared:**
- `repo-alignment-assessment.md` (existing, diagnostic)
- `alignment-assessment.md` (new, detailed + prescriptive)

---

## Summary: Both Reach Same Core Diagnosis

Both documents identify the same root problem: **core model is strong, but integration surfaces are incomplete and drift against each other.**

Where they differ is depth, scope, and prescription:

| Dimension | repo-alignment-assessment | alignment-assessment |
|-----------|---------------------------|----------------------|
| **Length** | ~180 lines | ~500 lines |
| **Focus** | Diagnostic (what's the state) | Prescriptive (here's what to fix) |
| **Scope** | High-level gaps | Detailed per-layer drift |
| **Phase** | Identify next slices | Recommend 3-phase sequencing |
| **Audience** | Director-level overview | Execution-level detail |

---

## Convergence: Top Issues Both Identify

### 1. No Single Stable Read Path (Highest Priority)
**repo-alignment-assessment:** Different files describe different default loading behavior (AGENTS.md vs. skills/llm-os-session vs. ops-model-delta). "Biggest live inconsistency."

**alignment-assessment:** Operating-model-update mode, read-path rules, and routing documented in ops-model-delta but not in AGENTS.md or skills. `/background` rule not enforced in entry points.

**Verdict:** Both say this breaks the "minimal context" promise. Needs immediate fix.

### 2. Mode Model Partially Normalized
**repo-alignment-assessment:** AGENTS.md defines new-project/existing-project/ongoing-session/operating-model-update, but ops-model-delta talks about execution/review without mapping them. Routing idea is good but not integrated.

**alignment-assessment:** Routing layer (Think→Plan→Build→Review→Ship→Reflect) is designed but not shown per-mode in AGENTS.md. No routing table.

**Verdict:** Modes and routing are related but not cleanly unified. Need single canonical mapping.

### 3. Entry-Surface Work Unfinished
**repo-alignment-assessment:** AGENTS.md, README, and skills/llm-os-session exist, but ASSISTANT.md is missing. Multi-entrypoint story is incomplete.

**alignment-assessment:** Doesn't explicitly flag ASSISTANT.md, but notes that no guidance exists for "what an ASSISTANT.md equivalent should look like."

**Verdict:** There's a missing entrypoint piece. Agreement on gap; unclear what the piece is yet.

### 4. Human-Interface Contracts Ahead of Skills
**repo-alignment-assessment:** Contracts defined (surface-uncertainty, critique-solution, package-decision) but not implemented as skills. Conceptual model describes more behavior than repo can invoke.

**alignment-assessment:** Same 3 contracts plus missing capture-human-input and surface-human-topics skills from next-slices.

**Verdict:** Human-side interaction layer is designed but not built. This is a "now" item that's incomplete.

### 5. Background/Reference Boundaries
**repo-alignment-assessment:** Concept is right (non-default context), but structure is loose. References to `/background` vs actual location `docs/background/`, and one planned slice still points to `/background/frameworks/...`

**alignment-assessment:** Doesn't explicitly address path inconsistency, but flags that read-path rule (don't load /background by default) isn't enforced in entry points.

**Verdict:** Both see boundary issues, different angles. Need clarity on structure and enforcement.

### 6. Repo is Template, Not Self-Hosted OS
**repo-alignment-assessment:** Project spine/milestone/questions/brief/report are templates, not filled in. Acceptable for scaffold but proof gap if goal is to show loop works end-to-end.

**alignment-assessment:** Same observation; calls it "ambiguous" whether docs should be filled in (if llm-os is also a project) or moved to templates (if pure framework).

**Verdict:** Same gap; both unsure what the intent is. This is a **key open question.**

---

## Divergence: Different Recommendations

### repo-alignment-assessment Recommendation:
> "Highest-value work now is not inventing more theory. It is collapsing the repo to one coherent operating surface around the current core."
>
> Focus on these near-term slices:
> 1. enforce one read path
> 2. normalize routing vs. modes
> 3. finish the entry-surface set
> 4. define the platform playbook
> 5. make the human-interface contracts real

**Philosophy:** Integration-first. Get the surface coherent, then fill in the scaffolding.

### alignment-assessment Recommendation:
> Complete Phase 1 (integration) before onboarding a project:
> 1. Update AGENTS.md with operating-model-update mode, read-path rule, routing table
> 2. Update all skill SKILL.md files to match updated AGENTS.md
> 3. Verify change-policy consistency
> 4. Add explicit clarification guidance to AGENTS.md
>
> Then Phase 2 (scaffolding):
> 1. Create core/platform-playbook.md
> 2. Define project-overview input schema
> 3. Design capture-human-input and surface-human-topics skills

**Philosophy:** Same (integration first) but more explicit about sequencing and dependencies.

**Convergence:** Both say integration before scaffolding. Alignment-assessment is more granular.

---

## Key Open Questions Both Raise (But Neither Fully Resolves)

### 1. How Should We Treat `/docs/background`?

**The tension:**
- `/background` is meant to be non-default context (not loaded unless needed)
- But many reference docs live there: next-slices, ops-model-delta, framework-comparison, alignment assessments
- These assessment docs themselves are now in `/docs/background/`
- The read-path rule says "do not load `/background` unless explicitly referenced" — but these assessments ARE important for decision-making

**Question:** Should background docs be:
- **Option A:** Non-discoverable (truly optional reference)?
- **Option B:** Discoverable in planning/review, but not in execution?
- **Option C:** Tiered (e.g., next-slices is discoverable; framework-comparison is not)?
- **Option D:** Move strategic docs (next-slices, ops-model-delta) out of `/background` into core docs?

**Current state:** Unclear. Both assessments reference `/background` docs heavily, which suggests they're important for coherence, not optional.

---

### 2. Should llm-os Instantiate Its Own Operating Model?

**The tension:**
- llm-os defines canonical project docs (spine, milestone, questions, brief, report)
- These are currently templates in `/docs/`
- It's unclear whether llm-os should be a "self-hosted" example (filled in) or pure framework (templates only)

**Option A: Self-Hosted (Fill in docs/)**
- ✓ Proves the loop works end-to-end
- ✓ Provides a reference example for users
- ✓ Forces discovery of gaps early
- ✗ Makes llm-os meta (system for managing the system)
- ✗ Creates ambiguity: is llm-os a project or a framework?

**Option B: Pure Framework (Move to core/templates/)**
- ✓ Keeps llm-os as a framework, not a project
- ✓ Cleaner abstraction boundary
- ✗ No worked example
- ✗ New users have no reference to compare against

**Option C: Hybrid (Create /docs/examples/ with minimal reference project)**
- ✓ Framework stays clean
- ✓ Example available but separate
- ✓ Could be synthetic or real
- ✗ Adds another directory

**Current state:** Ambiguous. This doc itself (alignment-assessment.md) is in `/docs/background/`, which raises the same question.

---

### 3. What Is ASSISTANT.md Supposed To Be?

**repo-alignment-assessment flags it as missing.**

Operating-model.md mentions "entry points" (Notion, repo, etc.) but doesn't say what ASSISTANT.md is or how it relates to the operating model.

**Possible interpretations:**
- Claude Code-specific instruction file?
- General multi-tool instruction template?
- List of all available agent contracts?
- Tool-specific output derived from AGENTS.md?
- Something else?

**Current state:** Not defined. This is a gap both docs identify but can't resolve without more context.

---

### 4. Should Routing (Think→Plan→Build→Review→Ship→Reflect) Be a Mode or a Pattern?

**repo-alignment-assessment:**
> "The routing idea is good, but it has not been fully integrated into the live mode model."

**alignment-assessment:**
> "Documented in ops-model-delta Δ1... [but] NOT shown in AGENTS.md"

**The question:**
- Is routing a top-level mode (like new-project, existing-project)?
- Is it a sub-lifecycle within each mode (optional depending on mode)?
- Is it implicit in every mode but expressed differently per mode?

**ops-model-delta suggests:**
> Δ5 shows routing per mode:
> - ongoing-session: Think → Build
> - execution: Build → Review → Ship
> - review: Review only
> - existing-project: Think → Plan
> - new-project: Think → Plan

So routing is a **pattern applied per-mode**, not a mode itself. But this isn't documented in AGENTS.md or any skill.

**Current state:** Designed but not integrated.

---

## Synthesis: Where the Assessments Agree to Act

Both documents converge on this priority order:

### Immediate (Must Fix to Unblock First Project)
1. **Enforce one read path** across AGENTS.md, skills, and templates
2. **Normalize modes and routing** — show how routing pattern applies per-mode
3. **Finish entry surface** — clarify what ASSISTANT.md is (or confirm it's not needed)
4. **Verify change-policy consistency** — all layers (core, entry, templates, skills) should align

### Near-Term (Scaffolding, "Now" Items from Next-Slices)
1. **Platform playbook** — tool usage, escalation, write-back expectations
2. **Human-interface skills** — surface-uncertainty, critique-solution, package-decision, capture-human-input, surface-human-topics
3. **Project-overview schema** — structured input for portfolio refresh
4. **Freshness model** — prevent doc drift (mentioned in next-slices)

### Medium-Term (Later Items)
- Stage skills expansion
- Schemas (YAML renditions)
- Human interaction workflow across entry points
- Engineering baseline (acceptance criteria, testing, observability)

---

## Recommended Next Steps

### Step 1: Resolve Open Questions (This Week)
Before starting Phase 1 integration work, clarify:

1. **Background boundaries:** Should next-slices and ops-model-delta stay in `/docs/background/`, move to `core/`, or get tiered access?
2. **Self-hosted OS vs. framework:** Should llm-os fill in its own project spine/milestone, or stay template-only?
3. **ASSISTANT.md:** Is this required for multi-entrypoint story, or out of scope?
4. **Routing as pattern vs. mode:** Confirm routing is sub-lifecycle per-mode, not a top-level mode itself.

**Decision maker:** You (Armin)  
**Write-back targets:** Answer in `/docs/open-questions.md` or a new decision doc

### Step 2: Update AGENTS.md (Phase 1)
Once Step 1 questions are answered:

1. Add routing table showing Think→Plan→Build→Review→Ship→Reflect per mode
2. Add operating-model-update mode with consistency-check trigger
3. Add explicit read-path guidance (including `/background` rule)
4. Update mode descriptions to reference routing table

**Effort:** 1-2 sessions  
**Blocker:** Step 1 questions must be resolved

### Step 3: Sync Entry Points (Phase 1)
1. Update skills/*/SKILL.md files to match updated AGENTS.md
2. Verify README.md, AGENTS.md, and skill descriptions don't contradict
3. Decide on ASSISTANT.md (create, skip, or clarify intent)

**Effort:** 1 session  
**Blocker:** Step 2 must complete

### Step 4: Fill "Now" Scaffolding (Phase 2)
1. Platform playbook (defines tool conventions, escalation, write-back)
2. Project-overview schema (for portfolio refresh skill)
3. Human-interface skill stubs (surface-uncertainty, critique-solution, package-decision)
4. Optionally: capture-human-input, surface-human-topics (OpenClaw-specific)

**Effort:** 2-3 sessions  
**Blocker:** Phase 1 complete

---

## Document Status & Recommendations

### repo-alignment-assessment
- **Status:** High-level diagnostic, well-written
- **Audience:** Decision/planning level
- **Keep?** Yes, as a reference. Provides good "what's the state" view.
- **Location:** Stays in `/docs/background/` (it's background analysis)

### alignment-assessment (New)
- **Status:** Detailed, prescriptive, layer-by-layer gap analysis
- **Audience:** Execution level (shows what to change where)
- **Keep?** Yes, as an actionable guide. Complements repo-alignment-assessment.
- **Location:** Stays in `/docs/background/` (it's detailed planning)

### This Comparison Doc
- **Purpose:** Highlight what the two agree on, note open questions, propose decision sequence
- **Keep?** Yes, as a decision checkpoint before Phase 1 starts
- **Location:** This doc should guide the next step: resolving Step 1 questions

---

## Key Insight from Both Assessments

Both documents agree on the **core thesis:**

> The operating model is sound. The implementation is incomplete. The next work is integration and scaffolding, not rethinking the model.

This is healthy. It means Phase 1 (sync entry points) and Phase 2 (fill scaffolding) are not fighting the design. They're finishing it.

The only prerequisite is clarity on the **open questions** (background boundaries, self-hosted vs. framework, ASSISTANT.md intent, routing pattern confirmation) so integration work doesn't re-decide design later.

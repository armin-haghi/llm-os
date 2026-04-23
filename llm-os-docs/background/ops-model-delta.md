Historical note: this delta note captures proposed changes from an earlier
design pass. Many of these items have since been integrated into the live
operating surface. File paths inside it may reflect older repo structure. Use
`AGENTS.md`, `core/platform-playbook.md`, and the live `core/` files as the
current source of truth.

## Δ Operating Model Enhancements (vNext Additions)

### Δ1. Execution Lifecycle (Routing Layer)

All work should implicitly follow:

```text
Think → Plan → Build → Review → Ship → Reflect
```

This is not a multi-agent system. It is a **routing discipline** applied within existing modes.

Usage guidance:
- Do not create separate agents per step
- Do not persist each step unless needed
- Apply implicitly during execution
- Applies consistently across all entry points (OpenClaw, Codex, Claude, repo edits, Notion), not tied to any single interface

---

### Δ2. New Mode: `operating-model-update`

Purpose:
- Modify system behavior (AGENTS.md, ASSISTANT.md, templates)

Rules:
- Must not be triggered during normal execution
- Must include:
  - reason for change
  - expected impact
  - affected modes/files
- Must be followed by a **consistency check**:
  - do existing modes still function?
  - does default read path change?

---

### Δ3. Default Read Path (Strict Enforcement)

Refine existing logic:

```text
1. AGENTS.md
2. Active milestone
3. Current task / plan
4. Relevant decision entries
5. Only then additional docs if required
```

Explicit rule:
- `/background` MUST NOT be loaded unless explicitly referenced
- when operating outside repo (e.g. Notion), equivalent minimal context should be used

---

### Δ4. Execution Constraints (Lightweight Guardrails)

During `execution` and `review`:

- Do not modify unrelated files
- Prefer smallest viable change
- Avoid introducing new abstractions unless required
- Clarify assumptions before implementation when unclear

---

### Δ5. Routing Clarification Within Modes

Modes remain unchanged, but must internally follow:

| Mode | Required Routing Emphasis |
|------|--------------------------|
| ongoing-session | Think → Build |
| execution | Build → Review → Ship |
| review | Review only |
| existing-project | Think → Plan |
| new-project | Think → Plan |

Notes:
- mapping applies conceptually even if the entry point does not explicitly expose ‘modes’

---

### Δ6. Background Folder Behavior

Introduce `/background`:

- Contains:
  - external frameworks (BMAD, gstack, etc.)
  - experiments
  - long-form references

Rules:
- Never loaded by default
- Only accessed when explicitly required
- Not part of execution context
- Applies only to repo-based context; equivalent ‘non-default reference material’ should be treated similarly in other tools

---

### Δ7. Borrowing Strategy (Explicit Constraint)

External frameworks are used as:
- **reference material**
- **pattern libraries**

NOT:
- direct operating models
- full workflow imports

All borrowings must:
- reduce complexity OR
- improve execution quality
- not introduce tool-specific coupling or expand default context

Otherwise: reject

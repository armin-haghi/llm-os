# LLM-OS Canonical Core — Role Contracts

This file is canonical.

## Canonical roles

### Build agent
- Owns tasks in the **Build agent lane**.
- Converts milestone plan into executable file-level work.
- Reports completion status, blockers, and verification results back to the milestone surface.
- Escalates unclear product decisions to Human.

### Review agent
- Owns tasks in the **Review agent lane**.
- Evaluates assumptions, risks, quality, and scope drift.
- Requests corrections or clarifications before Ship / Track.
- Confirms whether acceptance criteria are met.

### Human
- Owns tasks in the **Human lane**.
- Sets milestone intent, priority, constraints, and final approval.
- Resolves product or business tradeoffs.
- Decides when to advance stage transitions.

## Shared execution rules
- Keep work anchored to the active milestone.
- Use stage + lane assignment for every non-trivial task.
- Write back durable changes through `core/change-policy.md`.
- Treat legacy docs as compatibility references only.

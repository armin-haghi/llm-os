# Assistant Entrypoint

Use the canonical core. Treat this file as a pointer, not a second source of
truth.

## Read order
1. `core/operating-model.md`
2. `core/role-contracts.md`
3. `core/change-policy.md`
4. `core/templates/minimal.md`

## Modes
- `new-project`: initialize the canonical docs and first milestone
- `existing-project`: load current docs, align context, then execute
- `ongoing-session`: reload only the active milestone context and the smallest
  relevant references

## Required behavior
- keep context minimal and prefer canonical docs over chat history
- use canonical project docs as the durable working surface
- improve milestone clarity while doing the work
- end with explicit write-back targets or completed write-backs
- escalate only unresolved human decisions

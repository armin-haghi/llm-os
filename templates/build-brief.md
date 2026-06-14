# Build Brief

Use this to turn a problem or product idea into something a coding agent can build.

The brief has two parts:

1. **Product Build Brief** — what should be built and why.
2. **Agent Run Packet** — what the coding agent should read, change, test, and write back.

Keep it bounded to one milestone slice or one agent run.

---

## Part 1: Product Build Brief

### 1. Problem / business need

What breaks without this?

Who is affected?

What should be true when this works?

### 2. User journey

Happy path:

```txt
[Start state] → [Action] → [State] → [Action] → [End state]
```

Error paths:

- If:
  Then:
- If:
  Then:

### 3. Scope

In scope:

-

Non-goals:

-

### 4. Requirements

- R1:
  - Done when:
- R2:
  - Done when:
- R3:
  - Done when:

### 5. Components

| Component | Does | Input / trigger | Output / write |
|---|---|---|---|
|  |  |  |  |

### 6. Data shapes

```ts
type Example = {
  id: string;
};
```

### 7. Tech / architecture decisions

- Stack:
- Where this lives:
- External dependencies:
- Important defaults:

### 8. Build sequence

#### M1: [smallest useful slice]

Build:

-

Done when:

-

#### M2: [next slice]

Build:

-

Done when:

-

---

## Part 2: Agent Run Packet

### 1. Run goal

Build:

So that:

### 2. Required read path

- `AGENTS.md`
- `project-overview.yaml`
- `docs/current-milestone.md`
- `docs/session-brief.md`
- [other relevant files]

### 3. Files likely touched

-

### 4. Agent permissions

May change:

-

Must not change:

-

### 5. Environment

- Deploy target:
- Secrets required:
- Pre-conditions:
- Local commands:

### 6. Verification

Run:

```bash
# test / lint / typecheck / build commands
```

Manual check:

-

Evidence to report:

-

### 7. Write-back targets

Update before closing if project state changes:

- `docs/session-brief.md`
- `docs/current-milestone.md`
- `project-overview.yaml`
- Agent Run Queue record, if used

### 8. Final handoff format

```md
## What changed
-

## Files changed
-

## Tests run
-

## Evidence
-

## Blockers / human decisions needed
-

## Write-back completed
-

## Next recommended run
-
```

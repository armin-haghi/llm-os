# Framework comparison

Purpose: compare external approaches as reference material for `llm-os`.

This file belongs in `/background` and is not loaded by default.

| Approach | Best idea to borrow | Risk for `llm-os` | Fit |
|---|---|---|---|
| `llm-os` | Minimal repo-native operating model; stages, lanes, durable project docs, small context | Can become vague without routing and clear agent contracts | Base layer |
| BMAD Method | Lifecycle discipline; adaptive planning depth; analysis → planning → architecture → implementation | Too heavyweight; too many agents/workflows for solo/multi-tool use | Borrow selectively |
| gstack | Practical execution verbs: plan, review, QA, ship, retro; useful guardrails | Command-heavy; Claude Code/startup-product bias | Execution inspiration |
| HookDevAgents | Hook-based completion, tmux isolation, task list, deterministic recovery loop | Too implementation-specific; assumes OpenClaw as orchestrator and coding agents as workers | Automation inspiration |
| Karpathy-style coding rules | Keep changes small; avoid unrelated edits; clarify assumptions; reduce complexity | Not a full operating model | Guardrails |
| Aider-style loop | Tight edit/review/git loop | Weak on project memory and planning | Implementation layer |
| Claude/Codex tool-native instructions | Tool-local instructions close to execution | Fragmentation if each tool diverges | Derived outputs only |

## Synthesis

| Layer | Preferred source |
|---|---|
| Control plane | `llm-os` |
| Lifecycle discipline | BMAD |
| Execution language | gstack |
| Agent dispatch / completion automation | HookDevAgents |
| Coding guardrails | Karpathy-style rules |
| Tight implementation loop | Aider-style workflows |
| Tool-specific files | Derived from `AGENTS.md` |

## What to borrow now

| Source | Borrow | Do not borrow |
|---|---|---|
| BMAD | adaptive planning depth | full role/agent system |
| gstack | review / QA / ship / retro language | command framework |
| HookDevAgents | task list lifecycle, hook completion, deterministic recovery | OpenClaw-only architecture as default |
| Karpathy-style rules | small scoped edits, no unrelated changes | nothing structural |
| Claude/Codex | local instruction files | independent behavior definitions |

## HookDevAgents notes

HookDevAgents is useful because it solves a different layer: not the operating model itself, but **agent execution automation**.

Useful patterns:
- task list with simple lifecycle: `running → done / needs_attention`
- tmux sessions for detached coding work
- hooks/notifications instead of polling for happy-path completion
- deterministic recovery loop for dead sessions or timeouts
- orchestrator reviews results before reporting done
- minimal task schema

Caution:
- do not make OpenClaw the only entry point
- do not require tmux/hooks for normal work
- do not add automation until manual routing is stable

Best fit:
- later automation layer for dispatching Codex/Claude tasks
- not part of default read path
- not a replacement for `AGENTS.md`
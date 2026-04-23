# LLM-OS Canonical Core — Change Policy

This file is canonical.

## Promotion rule
Session output is durable only after write-back to a canonical artifact.

## Default write-back target
Write back to `docs/current-milestone.md` first.
This is the default surface for stage status, lane ownership, tasks, risks, and next actions.

## Secondary write-back targets (optional)
Use only when the default milestone surface is insufficient:
- `docs/decision-log.md`
- `docs/status-update.md`
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- corresponding Notion milestone page
- relevant GitHub issue or pull request

## Required change metadata
For non-trivial updates, include:
- stage affected
- lane owner (Human / Build agent / Review agent)
- task(s) updated
- next stage transition condition

## Drift rule
When Notion, repo docs, and GitHub disagree, update `docs/current-milestone.md` first, then reconcile outward.

## Legacy policy
Legacy docs are compatibility shims and must not act as competing policy sources.

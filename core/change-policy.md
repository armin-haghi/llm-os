# LLM-OS Minimal Core — Change Policy

This file is canonical.

## Promotion rule
Session output is durable only after it is written to at least one canonical target.

## Canonical write-back targets
- `docs/decision-log.md`
- `docs/status-update.md`
- `docs/current-milestone.md`
- `docs/handoffs/active-build.md`
- `docs/reviews/active-review.md`
- corresponding Notion milestone page
- relevant GitHub issue or pull request

## Drift rule
When Notion, repo docs, and GitHub disagree, explicitly flag drift and propose the single source to update first.

## Change hygiene
- Make the smallest change that resolves the current task.
- Keep previous operating-model docs as shims, not competing standards.
- Record migrations when old paths or behaviors are replaced.

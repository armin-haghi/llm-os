# Open Questions

| Question | Why it matters | Who should resolve it | Current default assumption | Decide by |
| --- | --- | --- | --- | --- |
| How aggressively should historical background analysis be rewritten after the first-cut cleanup? | It affects cleanup scope, doc drift, and how much historical material stays explicitly marked as time-scoped instead of being reconciled line by line. | Human | Keep historical assessment and delta docs mostly as historical notes; update only load-bearing references or add clear staleness framing. | After the next bulk of control-tower work |
| What is the minimum useful control-tower shape? | It determines whether the next slice improves cross-project visibility without becoming a second PM system or second source of truth. | Human | Keep the first control-tower slice minimal: project status, freshness, blockers, next decisions, and repo links only. | Before expanding beyond the first slice |
| What is the minimum durable checking method for future validation passes? | It affects how confidently llm-os can say that intent was met in practice instead of merely looking plausible to the maintainer. | Human | Accept the current validation pass, then define a lightweight rubric or check method as a follow-on rather than blocking the next slice on it. | During the control-tower milestone |

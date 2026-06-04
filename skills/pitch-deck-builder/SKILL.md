---
name: pitch-deck-builder
description: >
  Build a complete, polished pitch or reference deck from scratch. Use when the
  user asks to create a presentation, pitch deck, investor deck, co-founder
  deck, product overview, or any slide-based document intended for an external
  or semi-external audience. Also use when a deck needs to be rebuilt from
  existing content, when the user says "let's make a deck for X", or when they
  describe an audience and ask how to present a thesis, product, or opportunity.
  Prefer this skill over a generic PPTX skill for pitch or narrative decks.
---

# Pitch Deck Builder

Use this skill to produce an editable, shareable PPTX built with `pptxgenjs`.
The deck should have a clear narrative structure, self-contained slides, cited
figures, a verified glossary, and appendix slides for supporting detail.

Default source of truth for content is Notion when available. Keep repo-local
or workspace-local source material canonical if the user names another source.

## Core Rule

Front-load decisions before writing or building slides. The phases below are
sequential. Do not advance past a gate until the human approves that phase.

## Phase 0: Clarify

Ask these five questions in a single message. Do not proceed until all are
answered.

1. Audience: who reads this, and what do they already know?
2. Ask: what should the reader do or feel? Split by persona if needed.
3. Tone register: neutral internal reference, warm pitch, or confident
   opportunity statement?
4. Format: editable PPTX, PDF, or both?
5. Source context: Notion pages, repo docs, files, or other material to draw
   from?

## Phase 1: Source Setup

If Notion is available and relevant:
- fetch the main project Notion page before writing
- create or update one child page named `Deck - Content & Structure`
- append confirmed slide copy as each slide is approved
- mark each approved slide with `confirmed`
- flag visual ideas as callouts or a clearly labeled visual-notes block

If Notion is unavailable:
- use the user's named files or repo docs as the source context
- keep a local outline artifact only when the deck work needs durable
  intermediate state

## Phase 2: Narrative Spine

Identify the conceptual backbone before writing slide titles. Everything else
must support or resolve the spine.

Common spine forms:
- six-point failure-and-resolution framework
- before/after comparison with numbered matched items
- three forces converging
- one company proved it, nobody productized it

Gate: get explicit approval before writing slide content.

## Phase 3: Slide Structure

Propose the structure as:

```text
# | Headline | What this slide does
```

Rules:
- headline states the conclusion, not the topic label
- every headline should be informative to a cold reader with no context
- keep the main deck concise; move support detail to appendix

Standard sequence:

```text
Cover -> Setup -> Blueprint/problem -> Structural insight -> Why tools fail ->
Product -> Why now -> Market + competitive proof -> Business model ->
Proof/traction -> Ask by persona -> Glossary -> Appendix
```

Gate: get the structure approved before writing content.

## Phase 4: Design Selection

Propose design options before building. Do not pick unilaterally unless the
human asks you to choose.

Named presets:

| Preset | Palette | Best for |
| --- | --- | --- |
| Dark Editorial | `1E1E1E` background, white text, `2563EB` accent | technical, premium |
| Clean Analytical | `FFFFFF` background, `0F1E3C` navy titles, `1B4FBA` blue | analytical pitch quality |
| Split | `0F1E3C` dark cover, `FFFFFF` content, `D97706` amber accents | mixed strategy/product decks |
| Restrained Editorial | `F7F6F2` off-white, `1C1C1C` charcoal cover, `3D5A80` slate blue, `C2692A` amber | distinctive but restrained |

Default font specs:
- titles: Georgia 22-24pt bold
- labels: Calibri 14pt bold
- blueprint numbers: Georgia 15-17pt accent
- body: Calibri 13pt minimum
- tables: 10.5-11pt minimum

## Phase 5: Write Slide By Slide

Recommended writing order:

```text
Blueprint pair -> Cover -> Setup -> Insight -> Product -> Rest -> Appendix
```

Gate on each slide before writing the next.

Mandatory content rules:

- Self-contained: every slide reads cleanly without adjacent slides.
- Concrete examples: every analytical slide includes at least one real example
  in muted italic text.
- Blueprint structure: the framework appears twice, once as problem and once as
  resolution, with identical numbering and labels.
- Generic versus vertical: main deck blueprints stay generic unless the deck is
  explicitly vertical-specific; appendix slides may instantiate vertical
  examples.
- Persona split: create one ask slide per reader type, such as buyer,
  co-founder, or investor. Do not blend asks.
- Glossary: only include terms that appear in the main slides.
- Citations: every numeric claim needs a source. Verify math before using
  figures. Use in-slide superscripts and an appendix citations slide with
  links.
- Cross-references: validate every "see slide N" reference before build.

## Phase 6: Build

Use `pptxgenjs` with `LAYOUT_WIDE`.

Layout constants:

```javascript
const pptxgen = require('pptxgenjs');
const pres = new pptxgen();
pres.layout = 'LAYOUT_WIDE';

const ML = 0.72;
const MR = 0.72;
const CW = 11.89;
const TY = 0.28;
const TH = 0.92;
const CY = 1.28;

const COL3W = (CW - 0.4) / 3;
const col3x = (i) => ML + i * (COL3W + 0.2);

const COL2W = (CW - 0.35) / 2;
const col2x = (i) => ML + i * (COL2W + 0.35);
```

Technical rules:

| Issue | Rule |
| --- | --- |
| Empty bullets | use `breakLine: true` in the options array; do not concatenate `\n` into text |
| Complex visuals | generate as PNG with a plotting library and embed; avoid complex pptx shape construction |
| Text/image overlap | leave at least a 0.3 inch gap: `ML + textWidth + 0.3 <= imageX` |
| Column headers overlap intro | place headers at `startY`, not above it |
| Table overflow | leave a 0.3 inch buffer below tables because converters often render rows taller |
| Shadow corruption | never reuse mutable option objects; use a factory such as `makeShadow = () => ({ ... })` |
| File corruption | use hex colors without `#`, for example `1C1C1C` |
| Font too small | keep body text at 13pt minimum |

If the environment requires a global Node module path, initialize it explicitly
near the top of the build script:

```javascript
require('module').Module._initPaths();
```

## QA

Convert the PPTX to PDF and inspect every slide.

Example commands when LibreOffice and Poppler are available:

```bash
soffice --headless --convert-to pdf out.pptx
rm -f slide-*.jpg
pdftoppm -jpeg -r 150 out.pdf slide
```

If the environment provides a specialized PPTX validation helper, use that
helper instead of the generic `soffice` command.

Fix overflow, overlap, cut text, unreadable text, and broken citations. Run at
least one fix-and-verify cycle for each issue found.

## Phase 7: Deliver

Deliver the final PPTX, and PDF when requested, in the output location expected
by the current interface or repo workflow.

If Notion was used:
- mark approved slides as confirmed
- add a build notes section with output files, date, and remaining risks

## Optional Phases

Slide reduction pass:
- collapse into an adjacent slide or move to appendix
- do not silently delete content

Speaker notes:
- add two or three talking points per slide
- ask before building speaker notes

Adapt-to-vertical:
- keep slides such as insight, why now, model, and ask structurally identical
- instantiate blueprints, market, client engagement, and appendix examples
- add new appendix slides when needed

## Appendix Structure

Label appendix slides `A1`, `A2`, and so on. Use a footer such as:

```text
[Project] - Appendix
```

Standard appendix:
- A1: blueprint framework
- A2/A3: vertical worked example
- A4: alternative business model paths
- A5: source citations

## Common Failure Patterns

| Pattern | Fix |
| --- | --- |
| Two competing headlines | one title equals one conclusion; avoid kicker labels |
| Slide needs prior context | rewrite opener to be self-contained |
| Figures without sources | cite every number and verify the math |
| Glossary term not in deck | run a glossary verification pass |
| Blueprint labels diverge | lock numbered labels early and reuse them exactly |
| Design before structure | lock the structure before building with `pptxgenjs` |

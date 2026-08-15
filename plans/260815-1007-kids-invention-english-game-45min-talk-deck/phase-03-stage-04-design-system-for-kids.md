---
phase: 3
title: Stage 04 design system for kids
status: completed
priority: P1
dependencies:
  - 2
effort: 2h
---

# Phase 3: Stage 04 design system for kids

> **Superseded in part — 2026-08-15.** This phase was executed against the card-collecting product. The product then pivoted to a real-time game (see `plan.md` → *Revision*). The design principles below survived the pivot almost intact; two things changed in the shipped deck and `plan.md` is authoritative on both:
>
> - The colour principle is now *"the machine is the colour; everything else is workshop"*, and the density rule is *"six parts is the most that can ever be on screen"*.
> - **The failure rule split in two.** "No red, no buzzer, no timer" was a single rule here and would have made the game unbuildable. The shipped version separates *losing a round* (must be funny, one-tap restart) from *getting a word wrong* (never commented on at all).
>
> Also added after this phase: a fault must be identifiable without colour, and a round must be completable on a keyboard.

## Overview

Six slides. Carries forward every fix from the 2026-08-15 audit, and adds the constraints that only appear when the user is eight years old: reading level as a design token, 56px touch targets, and the hardest one — resisting the rainbow.

## Requirements

- Functional: design prompt outputs a DESIGN.md; screens prompt constrained to it.
- Content: all five audit carry-forwards present.
- Non-functional: 6 slides, ~7 min.

## Architecture

Slide order:

1. **Why this order** — "Make it look nice" has no memory (screens-first vs tokens-first cards). Verbatim from sibling deck.
2. **Tokens buy consistency. They do not buy taste.** Verbatim, with the default-palette card retargeted: for a kids' app the default the model reaches for is *rainbow primaries, Comic-Sans-adjacent rounding, and a mascot* — name it, forbid it.
3. **The design system prompt** — the corrected reusable prompt from the sibling deck (anti-feel, 5 principles, layout tokens, DO/DON'T, DESIGN.md output), with a Spark-specific `data-full` worked version.
4. **The kid constraints** — the slide that does not exist in the sibling deck. Four cards.
5. **Screens prompt** — constrained to the tokens, empty + error states, fold additions back into DESIGN.md.
6. **The token set** — Spark's actual tokens, with computed contrast ratios.

### The aesthetic commitment (slide 3's worked example)

> Should feel: curious, sturdy, handmade.
> Anti-feel: must NOT feel like a worksheet, and must NOT feel like a toy that talks down to me.

Five principles, each a decision with a consequence:

- **The cards are the colour; the app is the shelf.** A warm paper background and near-black text, so the only saturated colour on screen is the invention itself. This is the same content-first principle as a dark portfolio app, inverted for daylight and for children.
- **A surface ladder:** paper page, card, raised card when a card is being learned.
- **ONE accent**, reserved for "this is your next move" and nothing else. A kids' app that colours everything teaches a child that colour means nothing.
- **Geometry: generously rounded, never pill.** Cards are objects, and objects have corners.
- **Density: airy.** The opposite of the portfolio example. One card fills the screen; a child should never choose between six things at once.

### Slide 4 — the kid constraints (the new content)

| Card | Rule | Why |
|---|---|---|
| Touch | Minimum **56px**, not 44 | 44px is an adult finger on a phone. This is a child on a tablet, often lying down. |
| Reading | Body **18px minimum**, line-height 1.6, max 60 characters per line | A confident 8-year-old reader still tracks lines with a finger. |
| Reading level is a token | `--reading-max-words:40`, `--reading-cefr:"A2"` | The constraint has to live somewhere the *build* prompt can read it, or it gets lost between design and code. This is the token that Stage 05 feeds to Gemini. |
| Failure | No red, no buzzer, no timer | A wrong word match is a retry, not a mistake. The design system says so, so no screen invents a punishing state later. |

The fourth card is the one to say out loud: **accessibility for children is not a checklist item here, it is the product.** It also happens to be scored under Feasibility 40% in Stage 07.

### Slide 6 — the token set

Warm paper, one accent, big type. Include computed contrast ratios in a comment block, as the sibling deck does — the point is that the model was told to compute them, not assume them. Shape:

```
  --color-page:#FAF7F2;          --color-surface:#FFFFFF;
  --color-surface-raised:#FFFDF9;
  --color-text-primary:#1A1714;  --color-text-secondary:#5C544A;
  --color-border:#E4DCCF;        --color-brand:<one accent>;
  --color-success / --color-warning / --color-danger

  --font-stack:<a real fallback chain, no webfont>
  --text-display / title / subtitle / body(18px min) / small / micro + line-heights
  --space-1..6  ·  --radius-sm/md/lg (no pill)  ·  --shadow-1/2
  --container-max  ·  --bp-sm/md/lg  ·  --touch-min:56px  ·  --motion
  --reading-max-words:40  ·  --reading-cefr:"A2"
  /* contrast, computed not assumed: … all pass WCAG AA */
```

The accent is chosen during authoring, not pre-decided here — but it must be one colour, must not be the same hue as any invention card art, and the slide must carry the one-line reason, as the prompt demands.

## Related Code Files

- Modify: `docs/slides/kids-invention-game-pipeline-slides.html` — the `STAGE-04` block only
- Read only: `docs/slides/mvp-pipeline-prompting-slides.html` (corrected design prompt, tokens≠taste slide)

## Implementation Steps

1. Design divider (`Design` active in the stagerow).
2. "Why this order" slide — copy verbatim.
3. "Tokens ≠ taste" slide — copy, retarget the default-look card to the kids'-app default (rainbow, mascot, over-rounding).
4. Design system prompt slide — copy the corrected reusable prompt; write the Spark `data-full` worked version with the aesthetic commitment above.
5. Kid-constraints slide — `g2` × 2 rows of `.card sm`, per the table.
6. Screens prompt slide — copy verbatim including the "fold additions back into DESIGN.md" line.
7. Token slide — the `<pre>` above with real values and computed ratios.
8. Verify no slide exceeds 720px; the token slide is the likeliest to overflow — use `pre.sm` and abridge on-screen with the full set in `data-full`.

## Success Criteria

- [ ] 6 slides + divider in the `STAGE-04` block.
- [ ] DESIGN.md output requirement present in the prompt.
- [ ] `--touch-min:56px` and the reading-level tokens present and explained.
- [ ] The "tokens ≠ taste" slide names the kids'-app default and forbids it.
- [ ] Contrast ratios are stated as computed, and every pair passes AA.
- [ ] The accent has a stated one-line reason.
- [ ] No overflow.

## Risk Assessment

- **The token slide overflows.** Highest-risk slide in the deck. Abridge on screen, full set in `data-full`.
- **Rainbow creep.** If the authored token set has more than one saturated colour, the slide contradicts its own principle. Check before committing.
- **Reading-level tokens look like a gimmick.** Mitigation: slide 4's card must state the mechanism — Stage 05's prompt reads them — so it lands as plumbing, not decoration.

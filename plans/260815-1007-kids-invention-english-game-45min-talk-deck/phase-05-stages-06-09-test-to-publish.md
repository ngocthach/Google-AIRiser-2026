---
phase: 5
title: Stages 06-09 test to publish
status: completed
priority: P2
dependencies:
  - 4
effort: 1.5h
---

# Phase 5: Stages 06-09 test to publish

## Overview

Nine slides, ~10 min. Test, Evaluation, Deploy, Publish, plus recap and close. Compressed relative to the sibling deck — this is a talk, and the audience will copy these prompts rather than run them in the room.

## Requirements

- Functional: Test and Evaluation prompts copyable with full `data-full` versions.
- Content: failure modes must be child-specific, not generic.
- Non-functional: 9 slides, ~10 min.

## Architecture

### Test (2 slides)

Slide 1 — **Test for the demo, not for coverage**, reused, with one addition: the demo here has a second audience. A judge watches it; a child uses it. The child finds things the judge never will.

Slide 2 — the QA prompt, with Spark's demo steps and a child-specific failure list:

- The child taps the same card twice before it opens.
- The child gets a word wrong three times in a row — does the app punish them?
- The explanation comes back above their reading level anyway.
- Generation takes six seconds on venue wifi and the card looks broken.
- The parent signs in on a phone, the child plays on a tablet — same account, different device.
- The child closes the tab mid-card. Is that card collected, half-collected, or lost?
- Two children share one parent account. (Out of scope — but the *demo* must not fall over when it happens.)
- The tablet keyboard covers the word-match area.

Then: the 6-item pre-demo checklist, run in 3 minutes, in order.

### Evaluation (2 slides)

Slide 1 — the rubric: Feasibility 40% / Impact 30% / Creativity 30%, with one Spark-specific line under each:
- *Feasibility* — for a children's product, accessibility **is** feasibility: reading level, 56px targets, no timed pressure. Already built, now claim it.
- *Impact* — a child returning on day four is the only metric that matters. Say which one you can measure in a week.
- *Creativity* — "elegant use of AI" is not "we called an API". It is that the explanation adapts to the reader, and that the app costs nothing to run because it caches.

Slide 2 — the evaluation prompt, with Spark's "deliberately did NOT build" list carried down from the Stage 02 decision, and the harshness line kept verbatim.

### Deploy (1 slide)

Publish → name → live URL, plus the Starter Tier card and the "if it asks for a card" card. **Presenter note carries the same ⚠️ as the sibling deck:** publish a throwaway app from a fresh account the week of the talk; the `.ai.studio` / Starter Tier flow is not in current official docs, which describe Cloud Run and GitHub export. If the flow has moved, fix the slide before presenting.

Additional card specific to this deck: the app now has a database and an API key. State plainly that AI Studio holds the key server-side and never ships it to the client, and that the rules from Stage 05 are what make publishing safe.

### Publish (1 slide)

Merged from the sibling deck's two: the artifact table (project link / live URL / demo video / written scope) plus the 90-second video structure compressed to one row of four cards. The Spark-specific note: **film a child using it.** A 9-year-old collecting a card is a more persuasive 20 seconds than any narration.

### Recap + close (2 slides)

Slide 1 — where the hours go (the 18h task table from Stage 03, reframed as the recap), with the callout that stages 1-4 are a third of the time and produce no code.

Slide 2 — close. "Start at stage 01 tonight." Reuse the cover styling.

## Related Code Files

- Modify: `docs/slides/kids-invention-game-pipeline-slides.html` — the `STAGE-06-09` and `CLOSE` blocks
- Read only: `docs/slides/mvp-pipeline-prompting-slides.html`

## Implementation Steps

1. Test intro slide — `g3` cards (test hard / test some / skip) plus the two-audiences line.
2. Test prompt slide — abridged `<pre>`, full version in `data-full` with the child-specific list above.
3. Evaluation rubric slide — three `.card accent` with `.stat` percentages, each with its Spark line.
4. Evaluation prompt slide — abridged + `data-full`.
5. Deploy slide — `.flow` of 3 steps + `g2` cards; ⚠️ presenter note.
6. Publish slide — artifact table + `g4` video row; "film a child" callout.
7. Recap slide — hours table.
8. Close slide — `.cover` styling.
9. Overflow check across the block.

## Success Criteria

- [ ] 9 slides across `STAGE-06-09` and `CLOSE`.
- [ ] Test failure list is child-specific; at least 6 of the 8 listed items present.
- [ ] Rubric slide ties accessibility to Feasibility explicitly.
- [ ] Evaluation prompt's "deliberately did NOT build" matches the Stage 02 decision's NOT DOING line exactly.
- [ ] Deploy presenter note carries the ⚠️ verification warning.
- [ ] Publish slide names the difference between project link and live URL.
- [ ] No overflow.

## Risk Assessment

- **Compression makes Test/Eval feel like filler.** Mitigation: the child-specific failure list is the differentiator; if a slide has to go, cut the recap, not the QA prompt.
- **Deploy slide goes stale between planning and presenting.** Owned by the presenter note; cannot be fixed in the plan.
- **The NOT DOING list drifts** between Stage 02 and Stage 07. Phase 06's consistency sweep checks this pair specifically.

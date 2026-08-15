---
phase: 4
title: Stage 05 code Firebase and AI layers
status: completed
priority: P1
dependencies:
  - 3
effort: 3h
---

# Phase 4: Stage 05 code Firebase and AI layers

> **Superseded in part — 2026-08-15.** This phase was executed against the card-collecting product. The product then pivoted to a real-time game (see `plan.md` → *Revision*). The five-layer structure, the security-rules beat and the copyright beat all survived unchanged. What changed in the shipped deck:
>
> - L1 builds **the round** (machine, six labelled parts, faults, pressure gauge), not a shelf and a card.
> - Screens are Sign in / The Workshop / The Machine; data is `users/{uid}/machines/{machineId}` and `machines/{id}`.
> - The **caching argument got stronger**: it is no longer about cost, it is that a three-second fault timer cannot wait on a two-second API call. Writes happen at the *end* of a round, never during one.
> - L4 generates parts, fault strings and a harder vocabulary tier — not a paragraph.
>
> `plan.md` is authoritative.

## Overview

Eight slides, ~10 min — the largest block and the reason this deck exists as a separate artifact. The sibling deck's Code stage builds one screen with no login and no database. This one builds a real app across five layers, and each new layer carries a lesson the sibling deck cannot teach: security rules, AI-output caching, and image rights.

## Requirements

- Functional: five build prompts, each copyable, each inheriting the previous artifact.
- Content: Firestore rules, caching, and copyright each get an explicit on-slide beat.
- Non-functional: 8 slides, ~10 min.

## Architecture

### The five layers

| Layer | Builds | The lesson |
|---|---|---|
| L1 | Shelf + Card UI, local state, **tokens applied from the first message** | Tokens are not a later layer |
| L2 | Google sign-in, user doc on first login | Auth before data, always |
| L3 | Firestore read/write for collected cards | **Then immediately: the rules** |
| L4 | Gemini explanation + word pairs | **Generate once, store, serve** |
| L5 | Empty / loading / error / accessibility | Where generated UIs fall apart |

The existing "build in layers" flow slide handles L1-L4 with four steps; this deck needs five. Extend the `.flow` markup to five steps or split across two rows — five `.step` divs at 1280px is tight, so prefer four across with L5 as a following callout.

### Slide inventory

1. **Build in layers** — the five-layer flow, plus the corrected red callout ("tokens are not a later layer").
2. **L1 build prompt** — the corrected build prompt from the sibling deck, including the mandatory token-consumption block (`:root` in `index.css` + registered in the Tailwind theme, no raw hex, no arbitrary values, write DESIGN.md and re-read it). Abridged on screen, full in `data-full`.
3. **The image slide** — see below. Sits here because L1 is where the seed data appears.
4. **L2 + L3 prompt** — sign-in and Firestore, one slide, two prompts in the `data-full`.
5. **The rules slide** — see below. The beat immediately after data lands.
6. **L4 prompt — the AI layer** — with the caching requirement and the reading-level tokens flowing in from Stage 04.
7. **Design QA prompt** — carried forward verbatim from the sibling deck: screenshot back into Gemini, audit against DESIGN.md.
8. **L5 states** — brief; empty shelf, mid-generation, offline, and the no-punishment failure state the design system already forbade.

### Slide 3 — the image slide

> **The book is not your asset library.**

The DK *1000 Inventions & Discoveries* artwork is copyrighted. So is most invention photography a search returns. Three options, on screen:

- **Generate it.** AI Studio's Build agent generates images on demand — ask for them in the same prompt that seeds the cards. One line: *"generate the card art for each seeded invention; no grey placeholder boxes."*
- **Public domain.** Wikimedia Commons, the Science Museum Group's open licence images — check the licence per image, not per site.
- **Do not** screenshot the book. A submission that ships someone else's artwork is not a submission.

Callout: this is the kind of thing that disqualifies you *after* you have won, which is worse than not winning.

### Slide 5 — the rules slide

The technical beat of the deck. Firestore starts either in test mode (open, then expiring) or locked — and the model will happily build against an open database and never mention it. A children's app storing children's progress on an open database is the failure that ends the project.

On-screen prompt:

```
Lock my Firestore. Right now the rules are the default.

The data:
  users/{uid}                        one doc per signed-in parent account
  users/{uid}/collected/{invention}  that account's progress
  inventions/{id}                    seeded reference data, same for everyone

Write rules so that:
- a signed-in user can read and write only documents under their own uid
- nobody can read another user's documents, even signed in
- inventions/ is readable by any signed-in user and writable by nobody
- an unauthenticated request can do nothing at all

Then tell me the exact steps to test this in the Firebase console
rules playground, including the case that should FAIL.
```

The last line is the point: **rules you have not seen fail are not rules you have tested.**

Second card on the slide — Vietnamese law, since the audience is building for Vietnamese children: Decree 13/2023/ND-CP requires verified parental consent for the personal data of children under 16. That is *why* the parent signs in and the child never fills a form — the Research stage found it, the Plan encoded it, and the rules enforce it. Three stages agreeing is the deck's thesis in one slide.

### Slide 6 — the AI layer, and caching

```
Add the explanation to the Card screen.

When a card is opened for the first time, call the model once to produce:
- exactly 3 sentences explaining the invention, in English, at CEFR
  --reading-cefr, using at most --reading-max-words words total
- 5 word pairs drawn from those sentences, for the matching game

Then write both into inventions/{id} and serve every later view from
Firestore. Do not call the model when a cached version exists.

If the model returns more than --reading-max-words words, or a sentence
that fails the level, regenerate once, then fall back to the seeded blurb.
Show the child something readable in every case.
```

Two callouts:
- **Generate once, store, serve.** Per-view calls are the cost and latency mistake of every first build. Thirty children opening the same card is one generation, not thirty.
- **The reading-level tokens are doing real work.** `--reading-cefr` and `--reading-max-words` were written in Stage 04 and are read by a prompt in Stage 05. That is what "artifacts feed forward" means concretely.

## Related Code Files

- Modify: `docs/slides/kids-invention-game-pipeline-slides.html` — the `STAGE-05` block only
- Read only: `docs/slides/mvp-pipeline-prompting-slides.html` (corrected build prompt, design QA prompt, layer flow)

## Implementation Steps

1. Layer flow slide — 4 `.step` across + L5 as a callout; include the "tokens are not a later layer" red callout.
2. L1 prompt slide — copy the corrected build prompt; write the Spark `data-full` with real tokens from Phase 3 and the seeded invention list.
3. Image/copyright slide — `g3` of `.card`, plus the red callout.
4. L2+L3 prompt slide — abridged on screen, both full prompts in one `data-full` script.
5. Rules slide — the prompt above in a `<pre>`, plus the Decree 13 card and the "rules you have not seen fail" callout.
6. L4 prompt slide — the prompt above, plus the two callouts.
7. Design QA prompt slide — copy verbatim from the sibling deck.
8. L5 states slide — four short cards.
9. Overflow check on every slide in the block; slides 5 and 6 carry the most text.

## Success Criteria

- [ ] 8 slides in the `STAGE-05` block.
- [ ] Token-consumption block present in the L1 prompt, verbatim from the corrected sibling deck.
- [ ] Firestore rules prompt present, including the "show me the case that should FAIL" line.
- [ ] Decree 13/2023/ND-CP named, and tied to the parent-signs-in decision from Stage 01.
- [ ] Caching requirement present, with the fallback path when generation fails the reading level.
- [ ] `--reading-cefr` / `--reading-max-words` visibly cross from Stage 04 into a Stage 05 prompt.
- [ ] Copyright slide present with three concrete options.
- [ ] Design QA prompt carried forward.
- [ ] No overflow.

## Risk Assessment

- **Block overruns 10 min.** It is the densest. If cutting is needed, merge L5 states into the design QA slide — do not cut the rules or caching beats; they are why this deck exists.
- **Rules text becomes wrong.** Keep to the canonical owner-only pattern and let the prompt produce the syntax; do not hand-write a rules DSL on a slide that could go stale.
- **Legal claim precision.** State Decree 13/2023/ND-CP as the reason parental consent matters for under-16 data; do not extend into advice beyond that. If the presenter is unsure, the presenter note should say to describe it as a constraint they designed around, not a legal opinion.
- **Five steps do not fit the `.flow` row.** Pre-empted: four across, L5 as callout.

---
phase: 2
title: Stages 01-03 problem to decision
status: completed
priority: P1
dependencies:
  - 1
effort: 2h
---

# Phase 2: Stages 01-03 problem to decision

> **Superseded in part — 2026-08-15.** The dramatic arc of this block survived the pivot to a real-time game (see `plan.md` → *Revision*); the decision and plan artifacts below did not. In the shipped deck: the problem statement is now *"a child will replay one level of a game forty times; no child rereads a lesson"*, the idea is *English as the control scheme*, the screens are Sign in / The Workshop / The Machine, and KILLS IT became *"a slow reader loses every round in eight seconds"*. `plan.md` is authoritative.

## Overview

Eleven slides covering Research, Brainstorm and Plan. This is the block where the pipeline *discovers* Spark — the audience must watch the product get narrower and change shape, not watch it get announced.

## Requirements

- Functional: every prompt slide has a copy button; abridged prompts carry a `data-full` hidden version.
- Content: the age band (8-11) and the parent-signs-in decision must arrive as **outputs** of Research, not premises.
- Non-functional: 11 slides, ~14 min.

## Architecture

The block's dramatic arc, and the reason it works:

| Slide | Beat | Why it matters |
|---|---|---|
| Research divider | "Is the problem real?" | — |
| Research prompt | Generic 6-step prompt + 2 product-specific questions | Reusable skeleton |
| Worked example | Filled in for "kids quit English apps" | Attendee sees a real fill |
| What came back | **The pipeline narrows the audience and names the parent** | The payoff |
| Brainstorm divider | Diverge then converge, never together | — |
| Diverge prompt | 8 ideas, 2 per bucket | Forced variety |
| Converge prompt | Score 1-5, argue against my favourite | Brutality |
| The decision | 5 lines: CHOSEN / FOR / BECAUSE / KILLS IT / NOT DOING | The artifact |
| Plan divider | What, and built with what | — |
| Plan prompt | PART A HOW, PART B TASKS, sum the hours | Reused verbatim |
| The plan artifact | Spark's screens, stack, data model, task table | Feeds Stage 04 and 05 |

**The Research problem statement** (broad, so the game can be discovered):

> Kids start an English app, use it for three days, and stop. The app has streaks and points, but nothing in it is worth coming back to. Meanwhile the same kid will read the same book about how a rocket works four times.

**The two product-specific Research questions** — the equivalents of the Ươm Mầm deck's questions 7 and 8, and the slides where the product changes:

7. I wrote "kids" as one audience. Argue that this is wrong. What breaks if a 7-year-old and a 12-year-old use the same product? Name the single age band you would keep and what I lose by cutting the rest.
8. Who actually has to say yes for this to reach a child — the child, the parent, the teacher, or the school? Whoever it is, what do they need to see, and what does that force into the product itself?

**The "what came back" slide** is the most important in the block. Two cards:
- *What I asked for:* an English app for kids.
- *What the pipeline gave back:* ages 8-11 (reading independently, not yet phone-owning); the parent is the one who says yes, so sign-in is a parent screen and the child never sees a form; the killer assumption is that a child will accept an explanation they cannot fully read — which sets the reading-level constraint that Stage 04 turns into a type token and Stage 05 turns into a prompt constraint.

Then the callout: **the product changed before a line of code existed. That is the pipeline working.**

**The decision artifact:**

```
CHOSEN:    Spark - collect invention cards, learn the English inside them
FOR:       children aged 8-11 who read independently, and the parent who sets them up
BECAUSE:   the curiosity is already there for inventions; the English rides along
KILLS IT:  a child abandoning a card because the explanation is above their reading level
NOT DOING: leaderboards, audio, multiple children per account, offline
```

**The plan artifact:**

```
PART A - HOW
 Screens   Sign in   - a parent gets the child set up, once
           The Shelf - show what is collected, and make the next card obvious
           The Card  - teach one invention, then prove it stuck
 Stack     React (TypeScript) + Tailwind, every value a CSS variable
           Firebase Auth (Google) + Cloud Firestore
           @google/genai, current Flash model, key in AI Studio's secret
 Data      users/{uid}             displayName, ageBand, streakDays, lastPlayedAt
           users/{uid}/collected/  collectedAt, wordsCorrect, attempts
           inventions/{id}         name, year, imageUrl, blurb, words[]   (seeded)

PART B - TASKS
 T1  Shelf + Card UI, local state, tokens applied   5h   -      a card flips
 T2  Google sign-in + user doc on first login       3h   T1     shelf survives reload
 T3  Firestore read/write for collected cards       4h   T2     progress persists
 T4  Gemini explanation + word pairs, cached        4h   T3     a new card generates once
 T5  Security rules + publish + demo pass           2h   T1-T4  another account sees nothing
                                                   18h of a 20h budget

Cut to fit: streak counter (2h) - the shelf shows progress without it.
```

Note T5 bundles security rules with publish deliberately — it makes the point that rules are a shipping requirement, not a nice-to-have.

## Related Code Files

- Modify: `docs/slides/kids-invention-game-pipeline-slides.html` — the `STAGE-01-03` block only
- Read only: `docs/slides/mvp-pipeline-prompting-slides.html` (prompt skeletons to reuse verbatim)

## Implementation Steps

1. Research divider (reuse `.divider` + `.stagerow` markup, `Research` active).
2. Research prompt slide — the sibling deck's 6-step prompt verbatim, with the `[PROBLEM]`/`[AUDIENCE]` placeholders intact so it stays reusable.
3. Worked-example slide — abridged `<pre>` on screen, full version in a `<script type="text/plain" id="full-research-spark">`, including questions 7 and 8 and the "ask me 3 questions first" line.
4. "What came back" slide — two-card `g2` (stop/go styling), then the red callout.
5. Brainstorm divider.
6. Diverge prompt slide — verbatim, buckets A-D. *Merge candidate with slide 7 if Phase 06 needs time.*
7. Converge prompt slide — verbatim, criterion 4 callout ("demo in 60 seconds without explaining it first" — Spark passes; say so out loud).
8. Decision slide — the 5-line block above in a `<pre>` with a copy button, plus the PRD-expansion prompt as `data-full`.
9. Plan divider.
10. Plan prompt slide — verbatim from the sibling deck.
11. Plan artifact slide — the PART A/B block above, `data-copy-label="COPY TEMPLATE"`.

## Success Criteria

- [ ] 11 slides present in the `STAGE-01-03` block.
- [ ] Research questions 7 and 8 present and phrased as challenges to the user's framing.
- [ ] The "what came back" slide states the age band, the parent decision, and the reading-level assumption.
- [ ] The plan artifact's task hours sum to 18 and the stated budget is 20, with a named cut.
- [ ] Every `<pre>` copies; every `data-full` target resolves.
- [ ] No slide overflows.

## Risk Assessment

- **The discovery reads as staged.** Mitigation: the "what came back" slide must show something genuinely non-obvious — the parent-screen consequence is that; "kids are 8-11" alone is not.
- **Block runs long.** It has the most slides. The diverge/converge merge is the pre-agreed cut.
- **Drift from the sibling deck's prompts.** Copy the prompt text from the file, do not retype it.

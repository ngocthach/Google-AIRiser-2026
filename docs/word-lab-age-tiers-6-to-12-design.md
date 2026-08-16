# Word Lab across ages 6–12 — the scaffold dial

Extends `word-lab-scribblenauts-stem-english-game-build-prompts.md`, which was written for 9–12. This document replaces its age band, its property list, and its input model.

> **Note on scope:** the three input modes below are correct and unchanged, but they now live inside a **side-view walkable world**, not a puzzle card — see `word-lab-world-design.md`. The property gate is now the *traversal* system: the avatar cannot jump, so height must be summoned. The budget table at the bottom of this document is superseded by the one in the world design (~82h).

---

## The problem with "6 to 12"

The deck's own Research prompt exists to argue against exactly this ask — it is the question that killed "ages 6–22" for Ươm Mầm. A 6-year-old and a 12-year-old do not share a mechanic:

| | 6-year-old | 12-year-old |
|---|---|---|
| Reads the English brief | No | Yes |
| Types | Palms barely reach the home row | Fluently |
| English nouns known | 0–50 | 500–1500 |
| Property words | Sensory only (hot, big, soft) | Abstract (conductive, transparent) |

So do **not** build one game for 6–12. Build **one world with three input methods**, and let the child move between them.

Good news: this is not an invention. Pearson's Global Scale of English covers young learners **6–14 in one framework** precisely by scaffolding — *"structures and frameworks which are progressively removed or loosened as the child grows in proficiency"*, with descriptors like *"if provided with pictures"* and *"given a model"*. The tiers below are those descriptors, made into a dial.

---

## Three scaffold levels — named by what the child does, never by age

| Level | Input | English being exercised |
|---|---|---|
| **PICK** | Six picture cards, tap one. No text input at all. Word printed under each picture. | Recognition. Meeting the noun. |
| **BUILD** | A bank of 12 words above the input. Tap to fill it; typing allowed but never required. | Recognition → production. |
| **WRITE** | Empty input. Any English noun. | Free production. |

**Same puzzle, same scene, same property gate, three ways to answer.** This is one screen with a dial, not three games — which is what makes it affordable.

Typing research backs the boundary: palms rest comfortably on a keyboard around **6–7**, structured typing works from **7–8**, and crucially *"it is easier for a child to type words they already recognise."* BUILD is not a crutch, it is the correct order: recognise, then produce.

### The parent sets the starting level by capability, not age

At sign-up, three options — worded so nothing is demeaning:

- "Reads pictures, not words yet" → **PICK**
- "Reads short words" → **BUILD**
- "Reads sentences and can type" → **WRITE**

An 11-year-old with no English starts at BUILD without ever being told they are on the little-kid setting. That matters more than it sounds.

### Movement, and it is one-directional in tone

- **Three solves in a row without touching the bank** → offer the level up: *"Want to try it without the words?"* Offer, never force. Declining costs nothing and it does not ask again for five puzzles.
- **Three misses in a row** → the bank simply appears. No announcement, no dialog, no "let's make this easier". This is the scaffold already specified in Layer 5; it is the same code path.
- **Never demote a level.** The bank appearing is enough.

---

## The property ladder — 3 tiers × 10

The *puzzle* carries a property tier. The *child* carries a scaffold level. They usually move together; the Lab shows puzzles at the child's tier and one above.

**Tier A — SENSORY** (usually PICK): `big` `small` `hot` `cold` `wet` `dry` `soft` `hard` `heavy` `loud`

**Tier B — MECHANICAL** (usually BUILD): `long` `short` `rigid` `flexible` `floats` `sinks` `sharp` `hollow` `light` `round`

**Tier C — MATERIAL** (usually WRITE): `transparent` `opaque` `conducts electricity` `insulates` `magnetic` `absorbent` `waterproof` `heat-resistant` `gives light` `stretchy`

This is a real STEM progression — senses, then mechanics, then material science — and it maps onto exactly how young-learner English moves from concrete to abstract. One ladder, both subjects.

### Nine puzzles, three per tier

| Tier | Puzzle | Gate |
|---|---|---|
| A | The soup is cold | `hot` |
| A | The baby is crying on the floor | `soft` |
| A | Everything blew off the table | `heavy` |
| B | Cross the stream | `long` + `rigid` |
| B | Get the ball off the lake | `floats` |
| B | Carry water from the well | `hollow` |
| C | The plant is dying in the dark | `gives light` |
| C | The circuit is broken | `conducts electricity` |
| C | Get the key out of the acid | `magnetic` |

Tier A gates are deliberately **one property**. Two is already too much bookkeeping at six.

---

## What changes for the youngest, and one honest correction

**A 6-year-old cannot read the brief.** So at PICK the brief is icon-led: the scene, one large property icon (a flame for `hot`, a feather for `light`), and the English word beneath it. One short sentence at most.

**The correction:** the original NOT DOING list cut audio, and that was decided when "audio" meant recording, hosting and shipping files. It does not. `window.speechSynthesis` is built into every browser, free, offline, no API key, no bytes to host. **Read-aloud costs about 6 hours, not 20.**

That changes the answer. For ages 6–7, a read-aloud button on the brief and on the model's sentence is not polish — it is what makes the tier work at all. Move audio from NOT DOING to T10.

Remaining NOT DOING: no voice *input*, no multiplayer, no offline, no several children per account.

---

## Revised plan

| # | Delivers | h | Was |
|---|---|---|---|
| T1 | Puzzle screen with **three input modes** + three outcomes | 14 | 10 |
| T2 | The Lab: puzzle list, tier gating, word shelf | 8 | 7 |
| T3 | Sign-in + the capability question | 3 | 3 |
| T4 | Firestore: solved, words, scaffold level, tier | 7 | 6 |
| T5 | The judge + strict JSON + fallbacks | 9 | 9 |
| T6 | Cache + pre-seed, three tiers | 7 | 5 |
| T7 | **9 puzzles** authored: scenes, gates, card art | 16 | 8 |
| T8 | Movement rules: promote offer, silent bank | 5 | 4 |
| T9 | States, keyboard-only, greyscale check | 6 | 5 |
| T10 | **Browser read-aloud** (`speechSynthesis`) | 6 | — |
| T11 | Security rules + playground test + publish | 4 | 4 |
| | | **85h** | 58h |

**85 hours, against a 60-hour budget.** Three honest ways to land it:

| Option | Hours | What you get | What you lose |
|---|---|---|---|
| **Raise the budget to 85h** | 85 | The full 6–12 range, 9 puzzles | Three more weekends |
| **Ship 6 puzzles, 2 per tier** (recommended) | ~70 | Full 6–12 range, thinner content | Content depth, which is the cheapest thing to add later |
| **Drop PICK, ship 8–12** | ~62 | Fits the original budget | The 6–7 band entirely |

**Recommendation: ~70h, six puzzles, all three tiers.** The tier range *is* the pitch — a judge watching a 7-year-old and a 12-year-old play the same game at different rungs is the demo. Nine puzzles versus six changes nothing in that demo, and puzzles are the cheapest thing to add after launch. Content depth is a week-two problem; the scaffold dial is not.

---

## Layer 1 delta — the input modes

Replace the input section of Layer 1 with this. Everything else in that prompt stands.

```text
THE INPUT — build all three modes now, not later. The mode is a prop on
one component; do not build three screens.

Mode WRITE (default for this layer):
- One text input, --input-bg / --input-border / --radius, at least
  --input-min-height, placeholder "type one word in English"
- One button, --touch-min tall: "BUILD IT"

Mode BUILD:
- The same input, plus a bank of 12 word chips above it: --chip-bg,
  --chip-text, --radius-sm, each at least --touch-min tall.
- Tapping a chip fills the input. It does NOT submit — the child still
  presses BUILD IT.
- Of the 12, six satisfy the gate and six do not. A bank of only correct
  answers turns the puzzle into multiple choice and the child stops
  reading the brief.

Mode PICK:
- No text input at all. Six picture cards, each --touch-min square or
  larger, each showing the object and its English word underneath at
  --text-body.
- Tapping a card submits immediately. A six-year-old should not have to
  find a second button.
- Two of the six satisfy the gate.

All three modes share the same three outcomes and the same sentence
placement. Switching mode must never change the layout of the scene or
the brief above it — the child sees the same world, answered differently.

THE BRIEF adapts to the mode:
- WRITE and BUILD: the sentence, with the required properties as chips.
    "The stream is too wide to jump. I need something [LONG] and [RIGID]."
- PICK: the scene, one large property icon, and the English word beneath
  it. At most one short sentence. A six-year-old cannot read a brief in
  English, so the icon carries the meaning and the word rides along.

Add a read-aloud button beside the brief and beside every outcome
sentence, using the browser's built-in window.speechSynthesis. No audio
files, no API. It must be silent unless pressed.
```

---

## Where this lands on the rubric

**Impact 30%** gets meaningfully stronger. The measurable claim changes from *"children 9–12 produce English nouns"* to *"a family with a 7-year-old and an 11-year-old buys one thing"*, and the metric — words produced per child per week — is now comparable across a six-year age range on one scale. That is a real product, not a demo.

**Creativity 30%** is unchanged and still rests on the judge adjudicating against a fixed property ontology.

**Feasibility 40%** improves: read-aloud, picture-only input, and keyboard-only completion together mean the game is playable by a pre-reader, a non-typist, and a child using a screen reader. That is not a checklist — it is three real people who can now play.

---

## Open questions

1. Does the property tier need to be independent of the scaffold level? A 12-year-old beginner on BUILD probably wants Tier C content with Tier B support. Currently they move together, which may be wrong.
2. Six picture cards at Tier A — is two correct answers out of six the right ratio, or does a six-year-old need three?
3. `speechSynthesis` voice quality for English varies by device and can be poor on cheap Android tablets. Test on the actual hardware Vietnamese families use before relying on it.

# Word Lab — the world, not the card

> **To build it, go to `word-lab-runbook-paste-order.md`.** This document is the *why*; the runbook is the *what to paste*.

Supersedes the DESIGN.md section and the screen model of `word-lab-scribblenauts-stem-english-game-build-prompts.md`. The property gate, judge contract, cache and security rules from that document all stand. The age tiers from `word-lab-age-tiers-6-to-12-design.md` stand.

---

## What was wrong

The earlier prompts described a **static illustrated card with a text box under it**. That is a quiz with pictures. Scribblenauts is not that, and the difference is not decoration — it is where the game lives.

| Scribblenauts actually has | The card design had |
|---|---|
| A side-view world you walk through, camera panning | One fixed illustration |
| An avatar under the child's control | No avatar |
| Objects that spawn **into** the world and stay | An object that appears then vanishes |
| NPCs standing around with visible wants | An abstract "brief" |
| A notepad always within reach | A form field |
| Thick black outlines, flat saturated cartoon | "Warm paper, notebook sketch" — and an anti-feel that literally forbade cartoons |

The last row is the worst of it: the design system banned the exact aesthetic being asked for.

---

## The world

**One level, side view, about 2.5 screens wide.** A street, a two-floor building you can see into, a rooftop. Camera pans horizontally to follow the avatar. Hand-drawn fixed layout — not procedural, not tiled.

**The avatar walks. The avatar cannot jump.**

This is the single most important rule in the design, and it is what makes the whole thing hold together:

> Height must be **summoned**. To reach the rooftop you need something `TALL` and `RIGID` — a ladder, stairs, a tree. A rope is tall but not rigid, so it will not do.

The property gate stops being a quiz question and becomes **the traversal system**. And the anti-jetpack device from the research becomes structural rather than a rule bolted on: you cannot summon a jetpack because there is no flying, and you cannot climb a rope because rope is not rigid.

**Three NPCs**, each standing somewhere in the level with a thought bubble above their head showing a property icon. Walk up to one and their line appears in a speech bubble:

> *"I'm freezing. Bring me something **HOT**."*

The want *is* the property gate. That is how Scribblenauts framed things too — a person with a problem, not an exercise.

**The notepad** sits top-right, always visible, always one tap away — the same affordance as the original. Opening it gives the child PICK, BUILD or WRITE according to their scaffold level.

**Summoned objects land in the world and stay.** A puff of smoke, gravity, it lands on the ground or a platform, and it is still there in ten minutes. Walk into it to pick it up and carry it over your head; press drop to put it down. Carry it to the NPC and they take it. A star appears.

**Three stars opens the exit.** Next level.

---

## The scope guard — read this before estimating

A full Scribblenauts physics sandbox is not a 60-hour build; the original took a studio years and 22,800 hand-tuned objects. Three constraints make this version affordable without making it feel dead:

1. **Objects have gravity and ground collision. That is all.** No object-to-object collision, no stacking, no rotation, no ragdoll, no fluids. An object falls, it lands, it sits.
2. **Climbing is a flag, not physics.** When the judge accepts a word, it returns the properties that thing has. If those include `rigid` and `tall`, the object is tagged `climbable` and the avatar may walk up it. Nothing is simulated. This is the trick that buys the whole traversal system for almost nothing.
3. **No jumping, no combat, no vehicles, no weather.** Walking, carrying, climbing, giving. Four verbs.

---

## Art direction — replacing the notebook aesthetic

Should feel: **hand-drawn, chunky, alive.** Anti-feel: must NOT feel like a worksheet, and must NOT feel like a corporate flat-vector illustration.

- **Thick black outlines on everything**, roughly 3px, slightly wobbly, as if drawn with a marker.
- **Flat saturated fills.** No gradients, no bevels, no drop shadows — except one soft ellipse under anything standing on the ground.
- **Characters**: round heads, big simple eyes, minimal mouths, chunky limbs. Readable at thumbnail size.
- **The world is warm and busy; the UI is calm.** Cream paper panels with the same black outline, so the notepad reads as an object in the world rather than a browser widget.

```css
:root{
  /* the world */
  --color-sky:#A8DCF0;        --color-ground:#7EC850;
  --color-ink:#1A1A1A;        --outline-w:3px;
  --outline:var(--outline-w) solid var(--color-ink);
  --color-paper:#FFF8E7;      /* UI panels, speech bubbles, the notepad */
  --color-paper-2:#F2E7CE;
  --color-accent:#C43F10;     --color-on-accent:#FFFFFF;
  --color-star:#FFC629;
  --color-success:#157F4B;  --color-warning:#8A5200;

  --font-stack:"Atkinson Hyperlegible","Verdana",system-ui,sans-serif;
  --font-weight-regular:400;  --font-weight-bold:700;
  --text-display:34px;   --lh-display:1.2;
  --text-title:26px;     --lh-title:1.25;
  --text-subtitle:20px;  --lh-subtitle:1.35;
  --text-body:18px;      --lh-body:1.6;      /* a floor, not a default */
  --text-small:16px;     --lh-small:1.5;
  --measure-max:42ch;                        /* speech bubbles are narrow */

  --space-1:8px;  --space-2:16px; --space-3:24px;
  --space-4:32px; --space-5:48px; --space-6:64px;

  --radius-sm:8px; --radius:14px; --radius-lg:22px;
  --radius-circle:50%;        /* no pill value: not available on purpose */
  --shadow-ground:0 4px 0 rgba(26,26,26,.18);   /* the only shadow */

  --touch-min:56px;   --motion:200ms cubic-bezier(.2,.8,.2,1);
  --walk-speed:150px/s;   --gravity:900px/s2;
  --camera-ease:400ms;

  /* read by the judge call, not by CSS */
  --reading-max-words:25;  --reading-cefr:"A2";

  --bubble-bg:var(--color-paper);   --bubble-border:var(--outline);
  --notepad-bg:var(--color-paper);  --notepad-border:var(--outline);
  --chip-bg:var(--color-paper-2);   --chip-text:var(--color-ink);
  --verdict-accept:var(--color-success);
  --verdict-reject:var(--color-warning);   /* warning, never red */
  --focus-ring:3px solid var(--color-accent);
}
```

Contrast, computed not assumed — all pass WCAG AA:
ink on paper **16.4:1** · ink on sky **11.7:1** · accent on paper **4.9:1** · white on accent **5.2:1**.

**Why this accent:** the world is sky-blue and grass-green and terracotta. A deep burnt orange is the one colour that reads as "act on this" against all three, and it is the roof colour, so it belongs to the world rather than sitting on top of it.

### DON'T

1. No gradients, no bevels, no glows, no shadow except `--shadow-ground`.
2. No flat-vector corporate look — the outline must wobble.
3. A rejected word never uses red. Rejection is `--verdict-reject` amber.
4. No score, no percentage, no accuracy, no report card, no timer.
5. No pill geometry, no mascot narrator, no confetti on every success.

---

## Revised budget

One level, three NPCs, three input modes.

| # | Delivers | h |
|---|---|---|
| T1 | Level layout, horizontal camera pan, avatar walk | 12 |
| T2 | Notepad UI + the three input modes (PICK/BUILD/WRITE) | 12 |
| T3 | Summon: puff, gravity, land, persist, carry, drop | 10 |
| T4 | NPCs: thought bubbles, speech, accepting an item, stars | 8 |
| T5 | `climbable` flag + walking up a placed object | 5 |
| T6 | The judge + strict JSON + fallbacks | 9 |
| T7 | Judgement cache + pre-seeded answers | 7 |
| T8 | Firebase Auth + Firestore + the capability question | 9 |
| T9 | Art: level, ~40 object sprites, 3 NPCs, avatar | 16 |
| T10 | Browser read-aloud (`speechSynthesis`) | 4 |
| T11 | States, keyboard-only play, greyscale check | 6 |
| T12 | Security rules + playground test + publish | 4 |
| | | **102h** |

**102 hours.** That is the honest cost of a world instead of a card, and it is well past the 60 you started with. Three ways down:

| Option | Hours | The trade |
|---|---|---|
| Build it all | 102 | It is a real game. Six or seven weekends. |
| **Tap-to-give instead of carry/drop; 2 NPCs; generate object art on demand** | **~82** | Loses the pleasure of physically hauling a ladder across a street. Keeps walking, summoning, climbing, giving. |
| Go back to the card design | ~70 | Cheapest, and it is not Scribblenauts. |

**Recommendation: ~82h.** Carrying is lovely but it is the most bug-prone ten hours in the table, and the demo reads almost identically without it. **Do not cut climbing** — climbing is what makes the property gate a game mechanic instead of a quiz.

---

## Open questions

1. Does AI Studio's Build agent produce a usable side-scroller with camera panning in one prompt, or does the world need to arrive in two layers (static level first, then avatar and camera)? Worth one throwaway build before committing T1's 12 hours.
2. Object sprite count — 40 hand-generated, or generate on first summon and cache the image? The second is cheaper and more magical, but a child summoning `dragon` and waiting six seconds for art is worse than a placeholder.
3. Vertical space: the image shows a two-storey building. One level of climbing is enough for an MVP; two may be worth it purely because reaching a rooftop is a much better reward than reaching a shelf.

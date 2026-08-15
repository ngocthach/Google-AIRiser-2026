# Word Lab — the pipeline run, stage by stage, ending in a paste-ready AI Studio prompt

Built by running `docs/slides/kids-invention-game-pipeline-slides.html` on a new product. Each section is the **artifact** that stage produces; the next stage eats it. Jump to [Stage 05](#stage-05--the-build-prompts) for the thing you paste into AI Studio.

Grounding: `plans/reports/research-scribblenauts-mechanics-260815-1509-llm-property-gate-game-design-report.md`

> **Superseded in part — this is now a side-view world, not a puzzle card.** `word-lab-world-design.md` replaces the screen model (a walkable level with NPCs and summoned objects that persist, not a fixed illustration with a text box), the whole DESIGN.md token set (hand-drawn cartoon with thick black outlines — the old anti-feel wrongly forbade cartoons), and the budget (~82h). The judge contract, the cache, the security rules and the DON'T rules on scoring and rejection all stand.
>
> **Superseded in part — the age band is now 6–12, not 9–12.** `word-lab-age-tiers-6-to-12-design.md` replaces the age band, the property list (30 properties across 3 tiers, not 20 flat), the plan and budget (~70h, not 58h), and the input section of Layer 1 (three modes, not one). Everything else here — the judge contract, the cache, the DESIGN.md, the security rules, the DON'T list — stands unchanged. Build from the assembled prompt in `word-lab-layer-1-paste-into-ai-studio.md`, which already has the tier changes applied.

---

## The one-paragraph version

**Word Lab.** A puzzle shows a problem and names the *properties* needed to solve it — "the stream is too wide, I need something **LONG** and **RIGID**". The child types one English noun. The model rules on whether that thing really has those properties and says why in one sentence. `plank` works. `rope` is long but not rigid — and that sentence is the lesson. The English vocabulary being taught (*rigid, buoyant, transparent, conductive*) **is** the STEM content; the same word does both jobs.

**Why it is not just Scribblenauts with an LLM.** In 2009, five people spent six months hand-building 22,800 objects and the magic was *"it knows that word?!"*. A model knows every word for free, so that magic is worth nothing now. The magic moved to **adjudication** — and adjudication is what kills the jetpack problem that broke the original. Scribblenauts' own fix (solve it three times with different words) checked the *string*, so `Wings` / `Big Wings` / `Small Wings` beat it. A property check cannot be beaten by retyping.

---

## Stage 01 — Research artifact (the problem brief)

```
AS A CHILD WOULD SAY IT: "I know the words for the test but I can't
say anything real with them."
AS A PARENT WOULD SAY IT: "She can name fifty animals and cannot ask
for a glass of water."

THE SEGMENT THAT FEELS IT MOST: children 9-12 who have two or three
years of school English, can read a short sentence, and can type. They
have vocabulary they have never once used to get something done.

WHAT THEY DO TODAY INSTEAD: flashcard apps, extra classes, YouTube in
their own language, a parent testing them at dinner. All of it is
recognition. Almost none of it is production.

WHO HAS TO SAY YES: the parent. They need to see that the child is
producing English, not tapping multiple-choice, and that nothing about
their child leaves the app.

THE 3 ASSUMPTIONS THAT WOULD KILL IT:
1. That a 9-year-old will type English rather than give up. (Riskiest.)
2. That property words - rigid, buoyant, conductive - are learnable at
   this age and not just adult vocabulary in disguise.
3. That being told "a rope is long but not rigid" reads as interesting
   rather than as being marked wrong.

CHEAPEST TEST OF THE RISKIEST ONE, THIS WEEK, WITHOUT BUILDING:
Sit with four children. Show a drawing of a stream and say "I need
something long and stiff". Ask them to write one English word. Count
how many write anything at all, and how many write a real answer.
```

**What Research changed:** the age band moved from 8–11 to **9–12** — typing English is the mechanic, and 8-year-olds mostly cannot. The parent still signs in.

---

## Stage 02 — The decision

```
CHOSEN:    Word Lab - puzzles name the PROPERTIES you need, the child
           types an English noun, and the model rules on whether that
           thing really has them
FOR:       children 9-12 with two or three years of school English who
           can read a short sentence and type, and the parent who sets
           them up
BECAUSE:   they have vocabulary they have never used to get anything
           done, and a property gate forces production instead of
           recognition
KILLS IT:  a child who will not type, or a model that accepts
           everything and lets the property gate collapse
NOT DOING: free-form sandbox, drawing, voice, multiplayer, offline
```

Scored against the deck's converge criteria: one person / 60 hours **4** · acute pain **5** · come back unprompted **4** · demo in 60s without explaining **5** (a stream, a word, a plank, a crossing).

---

## Stage 03 — The plan

### PART A — HOW

**Screens (3)**

| Screen | Its one job |
|---|---|
| Sign in | A parent sets the child up, once. The child never sees it again. |
| The Lab | Show which puzzles are solved, what is next, and the child's growing word shelf. |
| The Puzzle | Make the child produce one English noun that satisfies the property gate. |

**Stack**

- React (TypeScript) + Tailwind, every value a CSS custom property
- Firebase Auth (Google) + Cloud Firestore
- `@google/genai`, current Flash model, key in AI Studio's server-side secret
- **No physics engine.** Each puzzle has one fixed scene and three authored outcomes (works / fails / fails funnily). The model supplies judgement and language, never art or simulation. This is the decision that makes it a 60-hour build.

**Data model**

```
users/{uid}                    displayName, ageBand, wordLevel      ← theirs
users/{uid}/solved/{puzzleId}  solvedAt, wordsUsed[], attempts      ← theirs
users/{uid}/words/{word}       firstUsedAt, properties[], timesUsed ← theirs
puzzles/{id}                   scene, brief, required[], examples[]   ← shared
judgements/{hash}              verdict, properties[], sentence        ← shared cache
```

`judgements/` is the important one: **once the model has ruled on a word, the ruling is permanent and free.** A child who notices `ladder` was accepted yesterday and rejected today stops trusting the game immediately.

### PART B — TASKS (60-hour budget)

| # | Delivers | h | Dep | Done when |
|---|---|---|---|---|
| T1 | Puzzle screen, input, three outcome states, local state | 10 | — | a typed word produces an outcome |
| T2 | The Lab: puzzle list, locked/solved, the word shelf | 7 | T1 | six puzzles, one playable |
| T3 | Google sign-in + user doc | 3 | T2 | progress survives a reload |
| T4 | Firestore: solved puzzles, word shelf, wordLevel | 6 | T3 | persists across devices |
| T5 | **The judge call** + strict JSON contract + fallbacks | 9 | T4 | rope is rejected, with a reason |
| T6 | `judgements/` cache + 30 pre-seeded answers per puzzle | 5 | T5 | a repeated word returns instantly |
| T7 | 6 puzzles authored: scene, brief, property gate, art | 8 | T1 | a real property ladder, one style |
| T8 | Word bank scaffold after two failed attempts | 4 | T5 | a stuck child is never stuck |
| T9 | States: empty lab, thinking, offline, keyboard-only | 5 | T1–T8 | a puzzle solvable on a keyboard |
| T10 | Security rules + playground test + publish | 4 | all | another account sees nothing |
| | | **61h** | | of a 60h budget |

**Over by 1h — so cut:** the word shelf's property filter (3h). The shelf still lists words; sorting them is a week-two problem. **New total 58h.**

**Most likely to overrun:** T5, the judge. When it does, the squeeze lands on T7 (puzzles). That is the right trade — **ship four puzzles with a judge you trust rather than six with one you do not.**

---

## Stage 04 — DESIGN.md

Should feel: **inventive, precise, hand-made.** Anti-feel: must NOT feel like a textbook, and must NOT feel like a cartoon that thinks I am six.

Five principles, each a decision with a consequence:

- **The scene is the colour; the lab is paper.** A warm paper page and ink-dark text, so the only saturated colour is the puzzle itself and the one accent.
- **A surface ladder:** paper page, card, and the input raised above both — because the input is where the whole game happens.
- **ONE accent, ink blue, reserved for "it is your turn to type" and nothing else.**
- **Rounded but never a pill.** This is a notebook, not a toy.
- **One puzzle fills the screen.** Never a grid of things to choose between while thinking.

```css
:root{
  /* the scene is the colour; the lab is paper */
  --color-page:#F7F5EF;            --color-surface:#FFFFFF;
  --color-surface-raised:#FFFDF8;
  --color-text-primary:#16181D;    --color-text-secondary:#585F6B;
  --color-border:#E0DCD2;
  --color-accent:#1F5FD0;          --color-on-accent:#FFFFFF;
  --color-success:#157F4B;  --color-warning:#8A5200;  --color-danger:#A32C1E;

  --font-stack:"Atkinson Hyperlegible","Verdana",system-ui,sans-serif;
  --font-weight-regular:400;  --font-weight-bold:700;
  --text-display:36px;   --lh-display:1.2;
  --text-title:26px;     --lh-title:1.25;
  --text-subtitle:20px;  --lh-subtitle:1.35;
  --text-body:18px;      --lh-body:1.6;     /* a floor, not a default */
  --text-small:16px;     --lh-small:1.5;
  --text-micro:14px;     --lh-micro:1.45;
  --measure-max:60ch;

  --space-1:8px;  --space-2:16px; --space-3:24px;
  --space-4:32px; --space-5:48px; --space-6:64px;

  --radius-sm:8px; --radius:12px; --radius-lg:18px; --radius-xl:24px;
  --radius-circle:50%;          /* no pill value: not available on purpose */
  --shadow-1:0 2px 6px rgba(22,24,29,.06);
  --shadow-2:0 14px 30px rgba(22,24,29,.12);

  --container-max:680px;   --grid-gap:var(--space-3);
  --bp-sm:480px;  --bp-md:768px;  --bp-lg:1024px;
  --touch-min:56px;        --motion:200ms cubic-bezier(.2,.8,.2,1);

  /* read by the judge call, not by CSS */
  --reading-max-words:25;  --reading-cefr:"A2";

  /* the round */
  --input-bg:var(--color-surface-raised);
  --input-border:2px solid var(--color-border);
  --input-focus-outline:3px solid var(--color-accent);
  --input-min-height:var(--touch-min);
  --verdict-accept:var(--color-success);
  --verdict-reject:var(--color-warning);   /* warning, never danger */
  --verdict-unknown:var(--color-text-secondary);
  --chip-bg:#EDEAE1;  --chip-text:var(--color-text-primary);
  --focus-ring:3px solid var(--color-accent);
}
```

Contrast, computed not assumed — all pass WCAG AA:
`text-primary` 16.3:1 · `text-secondary` 5.9:1 · `accent` 5.3:1 on page · white on accent 5.8:1 · success 4.6:1 · warning 5.9:1 · danger 6.6:1.

**Why ink blue:** the puzzle scenes are warm — paper, wood, water, rust. One cool blue can never be mistaken for part of a scene, so "your turn" is always unambiguous.

### DON'T — the defaults an AI reaches for, forbidden

1. No rainbow palette, no mascot, no confetti on every accept.
2. **A rejected word never uses `--color-danger`.** Rejection is `--verdict-reject`, warm amber. The child was not wrong, the object was.
3. No score, no percentage, no accuracy, no report card, ever.
4. No timer anywhere. Thinking is the activity.
5. No pill geometry.

---

## Stage 05 — The build prompts

Five layers. **Run them one at a time, in order, testing after each.** Paste layer 1 into AI Studio Build now.

### The judge contract (referenced by L3 — read it, it is the game)

The model may only use this fixed property list. Bounding it is what stops the gate collapsing:

`long` `short` `rigid` `flexible` `heavy` `light` `floats` `sinks` `transparent` `opaque` `conducts electricity` `insulates` `magnetic` `absorbent` `waterproof` `hollow` `sharp` `heat-resistant` `gives light` `stretchy`

---

### LAYER 1 — the round (paste this first)

```
Build "Word Lab", a browser puzzle game for children aged 9-12 learning
English. React (TypeScript) + Tailwind. This layer is UI and local state
only - no Firebase, no model call, no routing.

THE GAME
A puzzle shows a scene and a short brief that names the PROPERTIES needed
to solve it. The child types one English noun. The game rules on whether
that thing has those properties, shows the outcome, and explains why in
one sentence.

Use exactly these design tokens - introduce no colours, sizes or spacing
outside this set:

[paste the whole :root block from Stage 04 above]

HOW TO USE THEM - this part is not optional:
- Put them in index.css under :root, and register them in the Tailwind
  theme so every utility class resolves to a token.
- No raw hex and no arbitrary values anywhere in the markup: no
  bg-[#...], no p-[13px], no text-[15px].
- Write DESIGN.md to the project root containing this token set and the
  DON'T list below, and re-read it before every later change I ask for.

THE PUZZLE SCREEN - its job: make the child produce one English noun
that satisfies the property gate.

Layout, top to bottom, container --container-max:
- The scene illustration
- The brief at --text-subtitle, wrapped to --measure-max. The required
  properties appear inside it as chips: --chip-bg, --chip-text, bold,
  --radius-sm. Example brief:
    "The stream is too wide to jump. I need something [LONG] and [RIGID]."
- One text input, --input-bg / --input-border / --input-radius, at least
  --input-min-height, placeholder "type one word in English"
- One button, --touch-min tall: "BUILD IT"

THE THREE OUTCOMES - hardcode these for layer 1, no model call:
1. ACCEPT (try: plank, ladder, bamboo, door, surfboard)
   The object appears in the scene, the problem visibly resolves, and a
   sentence appears in --verdict-accept:
     "A plank is long and rigid, so it holds your weight."
   Then a "NEXT PUZZLE" button.
2. REJECT (try: rope, string, balloon, jetpack)
   The object appears and fails visibly and a little comically - the rope
   sags into the water - and a sentence appears in --verdict-reject:
     "A rope is long, but it is not rigid. It bends."
   The input clears and stays focused. The child tries again immediately.
   This is the most important moment in the game. It must not feel like
   being marked wrong. No red, no cross, no sound of failure, no counter.
3. UNKNOWN (anything else, or non-English)
   --verdict-unknown, "I don't know that word. Try another one."

RULES THE DESIGN SYSTEM ALREADY DECIDED - do not violate them:
- A rejected word never uses --color-danger. Rejection is amber.
- No score, no percentage, no accuracy, no report card, no timer.
- No mascot, no confetti, no rainbow palette, no pill geometry.

Seed with these six puzzles. Only puzzle 1 needs to be playable in this
layer; the rest are data.
  1. Cross the stream          needs: long + rigid
  2. The plant is dying in the dark   needs: gives light
  3. Carry water from the well        needs: hollow + waterproof
  4. The circuit is broken            needs: conducts electricity
  5. The window is missing            needs: transparent + rigid
  6. Get the key out of the acid      needs: magnetic

Generate the scene illustration for each puzzle - warm, precise, drawn
like a notebook sketch, one consistent style. No grey placeholder boxes.

ACCESSIBILITY: keyboard reachable, --focus-ring on every focusable
element, WCAG AA contrast, tap targets at least --touch-min. The whole
puzzle must be completable with a keyboard alone - type, Enter, Enter.

Output complete working code. No placeholders, no "add logic here".
```

### LAYER 2 — the Lab and the word shelf

```
Re-read DESIGN.md and use only what is in it. No raw hex, no arbitrary
values. Still no Firebase and no model call.

Add "The Lab" screen - its job: show which puzzles are solved, what is
next, and the child's growing word shelf.

- Puzzle list, one row each: number, title, and the property chips it
  needs. Solved rows carry a --verdict-accept mark. Locked rows use
  --color-text-secondary and are not tappable.
- Below it, THE WORD SHELF: every word the child has ever had accepted,
  as chips. Tapping a chip shows the sentence that was written about it.
  This is the child's own vocabulary, earned - it is the thing they will
  want to show a parent.
- Empty state, day one: one playable puzzle, five locked, and an empty
  shelf reading "Words you build will live here."

Tapping a puzzle opens it in place. Still no routing.
```

### LAYER 3 — the judge (the AI layer)

```
Re-read DESIGN.md. Now replace the hardcoded outcomes with a real call
to the model, using @google/genai on the Node backend. The API key stays
in AI Studio's server-side secret and never reaches the browser.

THE JUDGE. Given the child's word and the puzzle's required properties,
return ONLY this JSON, nothing around it:

{
  "verdict": "accept" | "reject" | "unknown",
  "properties": ["long","rigid"],
  "sentence": "A plank is long and rigid, so it holds your weight."
}

Rules for the judge, and they matter more than the code around them:

- "properties" may ONLY contain values from this fixed list:
  long, short, rigid, flexible, heavy, light, floats, sinks,
  transparent, opaque, conducts electricity, insulates, magnetic,
  absorbent, waterproof, hollow, sharp, heat-resistant, gives light,
  stretchy
  Never invent a property. If a thing's relevant property is not on the
  list, it is not part of this game.
- "accept" only when the word names a real, physical, everyday thing
  that genuinely has EVERY required property. Be strict. A generous
  judge destroys this game: if almost anything is accepted, the child
  learns that words do not mean anything in particular.
- "reject" when the thing is real but lacks at least one required
  property. The sentence must name what it HAS and what it LACKS, in
  that order, because that contrast is the entire lesson:
    "A rope is long, but it is not rigid. It bends."
- "unknown" for a made-up word, a word in another language, or a proper
  noun. Never guess.
- The sentence is at CEFR --reading-cefr, at most --reading-max-words
  words, one sentence, present tense, no exclamation marks, and never
  addresses the child's ability - it talks about the object, never about
  them. Never "good job", never "not quite", never "you were close".

Worked examples the judge must agree with, for gate "long + rigid":
  plank    -> accept, "A plank is long and rigid, so it holds your weight."
  ladder   -> accept, "A ladder is long and rigid, so you can walk across it."
  rope     -> reject, "A rope is long, but it is not rigid. It bends."
  balloon  -> reject, "A balloon is light, but it is not long or rigid."
  jetpack  -> reject, "A jetpack is not long or rigid. It is not a bridge."
  florb    -> unknown, "I don't know that word. Try another one."

FAILURE HANDLING - a child must never be stuck staring at a spinner:
- If the model returns malformed JSON, retry once, then fall back to
  "unknown" with the standard sentence.
- If the call takes longer than 4 seconds, show the thinking state and
  keep waiting; never show an error page.
- If the call fails entirely, fall back to the puzzle's pre-seeded
  answer list and only then to "unknown".

Show a thinking state while the call is in flight: the input stays
visible and keeps its text, the button reads "THINKING…" and is
disabled. Never clear what the child typed while they are waiting.
```

### LAYER 4 — Firestore, the cache, and the rules

```
Re-read DESIGN.md. Add Firebase Auth (Google) and Cloud Firestore.

SIGN IN is a PARENT screen, seen once at setup. Plain language, no game
styling. One button, --touch-min tall, and one line saying exactly what
is stored: which puzzles their child solved and which words they built,
and nothing else. On first sign-in create users/{uid} with displayName
and an ageBand the parent picks from three options.

Collections:
  users/{uid}                    displayName, ageBand, wordLevel
  users/{uid}/solved/{puzzleId}  solvedAt, wordsUsed[], attempts
  users/{uid}/words/{word}       firstUsedAt, properties[], timesUsed
  puzzles/{id}                   seeded reference data, shared
  judgements/{hash}              verdict, properties[], sentence, shared

THE CACHE, and it is not optional. Before calling the model, look up
judgements/{hash} where hash is the word plus the sorted required
properties. If it exists, use it and do not call the model.

Two reasons, and the second is the important one:
1. Cost and latency - a repeated word must return instantly.
2. CONSISTENCY. Once the model has ruled on a word, that ruling is
   permanent. A child who sees "ladder" accepted today and rejected
   tomorrow stops trusting the game, and they notice faster than an
   adult would.

Pre-seed judgements/ with about 30 likely answers per puzzle - the
obvious right ones and the obvious wrong ones - so most inputs never
reach the model at all.

Write to users/ at the END of a puzzle, not during typing.
If a read fails, show the Lab with puzzle one playable and a quiet
retry. A child is never blocked from playing by a failed read.

Then tell me plainly: with the rules currently on this project, who can
read this data? Do not fix it yet - I want to see the answer first.
```

Then, immediately after — do not skip this and do not let it wait until launch day:

```
Lock my Firestore. Right now the rules are the default.

Write rules so that:
- a signed-in user can read and write only documents under their own uid
- nobody can read another user's documents, even signed in
- puzzles/ is readable by any signed-in user and writable by nobody
- judgements/ is readable by any signed-in user; writes only from the
  server-side code, never from the browser
- an unauthenticated request can do nothing at all

Then tell me the exact steps to test this in the Firebase console rules
playground, including the case that should FAIL.
```

### LAYER 5 — the scaffold and the states

```
Re-read DESIGN.md.

THE WORD BANK SCAFFOLD. After two rejected attempts on the same puzzle,
show eight word chips below the input - six that satisfy the gate and
two that do not. Tapping one fills the input; it does not submit. The
child still presses BUILD IT.

The two wrong chips are deliberate. A bank of only correct answers turns
the puzzle into multiple choice and the child stops reading the brief.

Never show the bank before two attempts. A child who solves it alone
must never see it.

REMAINING STATES:
- Empty lab on day one
- Thinking, mid-judge
- Offline: the puzzle stays playable from the cache; say so plainly
- Keyboard only: type, Enter, Enter, all the way through a puzzle
- The parent's first launch, before any word exists

Finally: convert a screenshot of the puzzle screen to greyscale. If the
accept and reject sentences are indistinguishable without colour, fix it
- the verdict must be carried by the words and the layout, not the hue.
```

---

## Stage 05b — the design QA prompt, after it runs

```
Screenshot attached. Here is my DESIGN.md: [paste].

Audit the screenshot against it, harshly:
1. Every colour, size, spacing or radius on screen that is NOT in the
   token set. Name the element and the offending value.
2. Every DON'T that got violated. (rainbow, mascot, confetti, red for a
   rejection, score, timer, pill geometry)
3. Contrast: any text pair failing WCAG AA. Compute, do not assume.
4. Any tap target under 56px, any body text under 18px.
5. Read the rejection sentence as a nine-year-old. Does it comment on
   the object, or on me? If it comments on me, that is a bug.
6. Rate 1-5: does this look designed, or generated? One specific reason.

Then: the ONE prompt I should send AI Studio next to fix the worst.
```

---

## Where this scores

- **Feasibility 40%** — accessibility is the product: 18px floor, 56px targets, keyboard-only completion, verdicts readable in greyscale, no timer, no score.
- **Impact 30%** — the measurable metric is *words produced*, not lessons finished. A child who types 40 English nouns in a week has done something no flashcard app measures.
- **Creativity 30%** — the model is not writing a paragraph. It is **adjudicating against a fixed property ontology**, which is what makes the anti-jetpack gate possible at all. Scribblenauts' own fix was a string comparison and players beat it with `Big Wings`. A property check cannot be beaten by retyping. That is the sentence to say to a judge.

## Open questions

1. Judge latency in AI Studio — the cache is sized assuming most inputs never reach the model. Measure with a throwaway build before trusting T5's 9 hours.
2. Whether 20 properties is too many for six puzzles. Possibly ship 12.
3. Vietnamese input is treated as `unknown` with a nudge. If most children type Vietnamese first, that nudge becomes the main screen and needs designing properly rather than being an edge case.

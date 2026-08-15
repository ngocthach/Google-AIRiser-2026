# Word Lab — runbook: what to paste, in what order

Five build prompts, one review prompt, then publish. Each is complete and paste-ready.

**What this is not.** Pasting five prompts does not produce a finished game. Each layer needs several rounds of correction in the chat before it is right. The prompts stop you building in the wrong order and give you something precise to argue with when the agent drifts — they do not remove the work.

**Setup:** `ai.dev` → **Build** → new app. One prompt at a time. Test after every single one.

---

## The order

| # | Paste | Builds | Do not continue until |
|---|---|---|---|
| 1 | `word-lab-layer-1-paste-into-ai-studio.md` | The whole world: level, avatar, camera, notepad ×3 modes, summoning, climbing, 3 NPCs, stars | The 8 self-checks at the bottom of that file all pass |
| 2 | [Layer 2](#layer-2--the-judge) | Real model call replaces the hardcoded table | `rope` rejects *and still appears*; `florb` summons nothing |
| 3 | [Layer 3](#layer-3--sign-in-database-cache-word-shelf) | Google sign-in, Firestore, judgement cache, word shelf | Reload keeps stars; a repeated word returns instantly |
| 4 | [Layer 4](#layer-4--lock-the-database) | Security rules | You have watched a denied read fail |
| 5 | [Layer 5](#layer-5--states-and-polish) | Empty/offline/thinking states, read-aloud, mobile | Whole level playable on keyboard alone |
| — | [Design QA](#design-qa) | Nothing — it reviews | Run after 1, 2 and 5 |
| — | [Publish](#publish) | A live URL | A second Google account cannot see the first child's words |

**Do not reorder.** Layer 2 before Layer 1 is complete means debugging a judge inside a broken world. Layer 3 before Layer 2 means caching outcomes that do not exist yet.

---

## Layer 2 — the judge

The hard one. Expect to turn the strictness dial five or six times.

This layer also solves the art problem: **an arbitrary accepted word has no sprite.** The answer is not to generate art on demand — a six-year-old will not wait six seconds. Unknown-to-the-catalogue objects render as a labelled shape with the English word printed on it. Instant, consistent with the art style, and it reinforces the spelling.

```text
Re-read DESIGN.md. Replace the hardcoded word table with a real call to
the model using @google/genai on the Node backend. The API key stays in
AI Studio's server-side secret and never reaches the browser.

Keep the existing Judgement type exactly. The judge fills it.

THE JUDGE. Given the child's word and the NPC's `wants` array, return
ONLY this JSON, nothing around it:

{
  "verdict": "accept" | "reject" | "unknown",
  "properties": ["tall","rigid"],
  "size": "small" | "medium" | "tall",
  "sentence": "A ladder is tall and rigid, so you can climb it."
}

"properties" may ONLY contain values from the PropertyId union already
in the code - the 30 ids across the sensory, mechanical and material
tiers. Never invent a property. If a thing's relevant property is not on
that list, it is not part of this game.

"size" is the object's rough real-world height:
  small  - fits in a hand        (coin, soup, ice, apple)
  medium - knee to chest high    (fire, stick, chair, dog)
  tall   - taller than a person  (ladder, tree, stairs, lamp post)

RULES:
- "accept" only when the word names a real, physical, everyday thing
  that genuinely has EVERY property in `wants`. Be strict. A generous
  judge destroys this game: if almost anything is accepted, the child
  learns that words do not mean anything in particular.
- "reject" when the thing is real but lacks at least one required
  property. The sentence names what it HAS and then what it LACKS, in
  that order, because that contrast is the entire lesson:
    "A rope is tall, but it is not rigid. It bends."
- "unknown" for a made-up word, a word in another language, or a proper
  noun. Never guess.
- The sentence is at CEFR --reading-cefr, at most --reading-max-words
  words, ONE sentence, present tense, no exclamation marks. It describes
  the OBJECT and never the child. Never "good job", never "not quite",
  never "you were close", never "try again".
- Even on "reject", fill "properties" with what the thing actually HAS.
  The world reads those flags.

Worked examples the judge must agree with, gate ['tall','rigid']:
  ladder  -> accept, ['tall','rigid'], tall,   "A ladder is tall and rigid, so you can climb it."
  tree    -> accept, ['tall','rigid'], tall,   "A tree is tall and rigid. You can climb the trunk."
  rope    -> reject, ['tall','flexible'], tall,"A rope is tall, but it is not rigid. It bends."
  balloon -> reject, ['light','round'], small, "A balloon is light, but it is not tall or rigid."
  jetpack -> reject, ['heavy'], medium,        "A jetpack is not tall or rigid. You cannot climb it."
  florb   -> unknown, [], small,               "I do not know that word. Try another one."

THE PROPERTIES DRIVE THE WORLD, not just the verdict. Read the flags off
the judge's answer; do not hardcode behaviour per word:
- 'tall' AND 'rigid'  -> climbable = true
- 'hot'               -> the sprite gets a soft warm glow and satisfies a hot want
- 'gives light'       -> a soft light halo
- 'floats'            -> rests on a water surface instead of passing through
This is the point of the whole design: the English word decides what the
object DOES.

SPRITES FOR UNKNOWN OBJECTS - solve it this way, do not generate images
at runtime:
- If the word is in the existing art catalogue, use that sprite.
- Otherwise render a LABELLED SHAPE: a plain rounded rectangle at the
  right SizeClass, --color-paper-2 fill, --outline border, with the
  English word centred on it in --font-stack bold at --text-body,
  --color-ink, wrapped to fit.
This is instant, matches the art style, and printing the word on the
object reinforces the spelling. A child summoning `dragon` gets a boxy
thing that says DRAGON, and that is honest and charming. Do not show a
loading spinner in the world and do not call an image model.

REJECTED WORDS STILL SUMMON, exactly as in Layer 1. Only 'unknown'
summons nothing.

FAILURE HANDLING - a child must never be stuck watching a spinner:
- Malformed JSON: retry once, then fall back to verdict 'unknown'.
- Slower than 4 seconds: keep the thinking state and keep waiting. Never
  show an error page.
- Call fails entirely: fall back to the Layer 1 hardcoded table, then to
  'unknown'. Keep that table in the code as the offline fallback.

THINKING STATE: the notepad stays open, the typed word stays visible,
the button reads "THINKING..." and is disabled. Never clear what the
child typed while they wait.
```

**Check:** `rope` rejects and still lands. `jetpack` rejects — that is the anti-jetpack device working. `dragon` gets a labelled box. Type something in Vietnamese: it must come back `unknown`, not a guess.

---

## Layer 3 — sign-in, database, cache, word shelf

### Do this in the Firebase console BEFORE pasting the prompt

The generated code will reference `GOOGLE_WEB_CLIENT_ID` and several `FIREBASE_*` values, and AI Studio's Secrets panel will list them as empty. They come from here, not from AI Studio.

1. `console.firebase.google.com` → create a project.
2. **Authentication → Get started → Sign-in method → Google → Enable**, pick a support email, Save. This auto-creates the OAuth web client for you.
3. On that same panel expand **Web SDK configuration** and copy the **Web client ID** → this is `GOOGLE_WEB_CLIENT_ID`.
4. **Project settings → General → Your apps → Web app** → copy `apiKey`, `authDomain`, `projectId`, `appId`.
5. **Authentication → Settings → Authorized domains** → add the domain AI Studio publishes to.
6. **Google Cloud Console → APIs & Services → Credentials** → open that OAuth client → add **both** the AI Studio preview origin and the published origin under *Authorized JavaScript origins*.
7. **OAuth consent screen** → either press **Publish app**, or add every email that will ever sign in (including the judges') under *Test users*.

Two traps, both of which bite on demo day:

- **Missing JavaScript origin** → `origin is not allowed`. The single most common failure. Add both origins in step 6.
- **Consent screen left in Testing** → only listed test users can sign in; everyone else gets an error page. A judge opening your link and being blocked is an avoidable way to lose.

`GOOGLE_WEB_CLIENT_ID` is **not a secret** — it ships in the browser bundle and that is fine. `GEMINI_API_KEY` *is* a secret and must stay server-side. Do not treat them the same way.

### Then paste this

```text
Re-read DESIGN.md. Add Firebase Auth (Google) and Cloud Firestore.

SIGN IN is a PARENT screen, seen once at setup; the child never sees it
again. Plain language, no game styling, no cartoon characters. One
button at least --touch-min tall, and one line saying exactly what is
stored: which levels their child finished and which words they built,
and nothing else.

On first sign-in ask the parent ONE question - the child's starting
level, worded by capability and never by age:
  "Reads pictures, not words yet"  -> PICK
  "Reads short words"              -> BUILD
  "Reads sentences and can type"   -> WRITE
Store as scaffoldLevel. It sets the notepad's default input mode.

Collections:
  users/{uid}                    displayName, scaffoldLevel
  users/{uid}/levels/{levelId}   completedAt, stars, wordsUsed[]
  users/{uid}/words/{word}       firstUsedAt, properties[], timesUsed, sentence
  levels/{id}                    seeded reference data, shared
  judgements/{hash}              verdict, properties[], size, sentence, shared

THE CACHE, and it is not optional. Before calling the model, look up
judgements/{hash} where hash is the lowercased trimmed word plus the
sorted `wants` array joined by '+'. If it exists, use it and do not call
the model.

Two reasons, and the second matters more:
1. Cost and latency - a repeated word must return instantly.
2. CONSISTENCY. Once the model has ruled on a word, that ruling is
   permanent. A child who sees "ladder" accepted today and rejected
   tomorrow stops trusting the game, and they notice faster than an
   adult does.

Pre-seed judgements/ with about 30 likely answers per NPC want - the
obvious right ones and the obvious wrong ones - so most inputs never
reach the model at all.

THE WORD SHELF: a second tab on the notepad listing every word the child
has ever had accepted, as chips. Tapping a chip shows the sentence that
was written about it and the properties it has. This is the child's own
vocabulary, earned - it is the thing they will want to show a parent.
Empty state: "Words you make will live here."

Write to users/ when a level completes and when a new word is first
accepted. Never on every frame.
If a read fails, start the level anyway with everything playable and a
quiet retry. A child is never blocked from playing by a failed read.

SCAFFOLD MOVEMENT:
- Three wants solved in a row without touching the word bank -> offer
  the next mode up: "Want to try it without the words?" Offer, never
  force. If declined, do not ask again for five wants.
- Three failed attempts on one want -> the word bank simply appears. No
  announcement, no dialog, no "let's make this easier".
- Never move a child down a mode. The bank appearing is enough.

Then tell me plainly: with the rules currently on this project, who can
read this data? Do not fix it yet - I want to see the answer first.
```

**Check:** sign out and back in; stars survive. Summon the same word twice — the second is instant. Open the word shelf.

---

## Layer 4 — lock the database

Paste immediately after Layer 3 answers the question. Do not leave this until launch day.

```text
Lock my Firestore. Right now the rules are the default.

The data:
  users/{uid}                    one doc per signed-in parent account
  users/{uid}/levels/{levelId}   that account's progress
  users/{uid}/words/{word}       that child's vocabulary
  levels/{id}                    seeded reference data, same for everyone
  judgements/{hash}              shared cache of model rulings

Write rules so that:
- a signed-in user can read and write only documents under their own uid
- nobody can read another user's documents, even signed in
- levels/ is readable by any signed-in user and writable by nobody
- judgements/ is readable by any signed-in user; writes only from the
  server-side code, never from the browser
- an unauthenticated request can do nothing at all

Then tell me the exact steps to test this in the Firebase console rules
playground, including the case that should FAIL.
```

**Check:** run the failing case yourself in the playground. Rules you have not watched fail are not rules you have tested.

---

## Layer 5 — states and polish

```text
Re-read DESIGN.md. Add the remaining states and invent no new tokens.

- First launch, before any word exists: the level plays normally; the
  word shelf reads "Words you make will live here."
- Thinking, mid-judge: as specified in Layer 2.
- Offline: the level stays playable from the cache and the hardcoded
  fallback table. Say so in one plain sentence. Never an error page.
- Level complete: the panel from Layer 1. No rating, no timer.

READ-ALOUD everywhere: a button on every speech bubble and every outcome
sentence, using window.speechSynthesis. Silent unless pressed. This is
what makes the game work for a six-year-old who cannot read the want.

KEYBOARD: the whole level completable with the keyboard alone - arrows
to walk, N for the notepad, type, Enter to summon, E to pick up and
drop, Up/Down to climb, Enter to give. --focus-ring on everything
focusable. Opening the notepad moves focus into the input; closing it
returns focus to the notepad button.

MOBILE: press and hold the left or right third of the screen to walk.
Pick-up, drop and give become one context button that appears at the
bottom-right when an action is in range. The notepad must not be covered
by the on-screen keyboard when it opens.

GREYSCALE: convert a screenshot to greyscale. If an accepted and a
rejected outcome look the same, fix it. The sentence must carry the
verdict; colour only reinforces it.

REDUCED MOTION: honour prefers-reduced-motion by removing the camera
easing and the star spin, keeping everything else.
```

---

## Design QA

Not a build prompt. Screenshot the game, open a normal Gemini chat, paste this.

```text
Screenshot attached. Here is my DESIGN.md: [paste the file].

Audit the screenshot against it, harshly:
1. Every colour, size, spacing or radius on screen that is NOT in the
   token set. Name the element and the offending value.
2. Every DON'T violated: gradients, glows, shadows other than
   --shadow-ground, flat corporate vector look, red for a rejection,
   score, percentage, timer, pill geometry, mascot narrator.
3. Contrast: any text pair failing WCAG AA. Compute, do not assume.
4. Any tap target under 56px, any text under 16px.
5. Read the rejection sentence as a seven-year-old. Does it talk about
   the object, or about me? If it is about me, that is a bug.
6. Rate 1-5: does this look hand-drawn and alive, or generated? Justify
   with one specific thing on screen.

Then: the ONE prompt I should send AI Studio next to fix the worst.
```

---

## Publish

Top right → **Publish** → set name and URL. Then:

1. Open the live URL on a phone you did not build on.
2. Play the whole level as a stranger would.
3. Sign in with a **second** Google account and confirm you cannot see the first child's words. That is the security rules working, and it is what you show a judge.

⚠️ **Verify the publish flow the week you need it.** The free-tier route moves. If it asks for a credit card you are not on it — try a Google account that has never published before.

---

## When it breaks

**The world misbehaves:**

```text
Here is what I did, step by step: [1... 2... 3...]
Here is what I expected: [...]
Here is what happened: [...]
Do not rewrite the file. Find the specific cause first, tell me what it
is in one sentence, and only then show me the smallest fix.
```

**The judge is too generous** — the most likely real failure:

```text
The judge accepted [word] for the gate [properties] and it should not
have. Tighten the judge prompt so this case rejects, WITHOUT making it
reject [three words that must still be accepted].
Show me only the changed prompt text, not the whole file.
```

**AI Studio asks for a secret you did not expect** — most often `GOOGLE_WEB_CLIENT_ID` during Layer 1:

```text
Remove Google sign-in entirely. Section "ARCHITECTURE" of my brief says
this layer is the world and local state only: no Firebase, no auth, no
model call. Delete that dependency and any auth UI, and do not add
authentication until I ask for it.
```

Auth belongs in Layer 3. Adding it early buys you OAuth configuration problems while you still have a camera bug.

**The game stutters:**

```text
The game stutters while walking. Confirm the animation loop mutates refs
and sets element.style.transform directly, and that no setState is
called per frame. If any component re-renders during movement, show me
which one and move its state into the ref object.
```

**It ignored the spec:**

```text
Section [X] of my brief specifies [quote it exactly]. The current code
does [what it does]. Change it to match the brief. Do not redesign
anything else.
```

---

## Honest expectations

- **Layer 1 is the hardest to get looking right.** A side-scroller with a panning camera is where AI Studio needs the most rounds. The spec gives you exact numbers to quote back when it drifts — use them rather than re-describing.
- **Layer 2 is the hardest to get *behaving* right.** Judge strictness is a dial, not a setting.
- **The art will be inconsistent at first.** Ask for all sprites to be regenerated in one message rather than fixing them one at a time; style consistency comes from a single generation pass.
- **Do not add a second level until one level is genuinely fun.** Content is the cheapest thing to add later and the most tempting thing to add too early.

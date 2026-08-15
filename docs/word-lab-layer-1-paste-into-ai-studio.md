# Word Lab — Layer 1, spec-grade. Copy the block below into AI Studio Build.

**This is step 1 of 6. Start at `word-lab-runbook-paste-order.md`.**

Builds the playable world: level geometry, walking avatar, camera, notepad with three input modes, summoning with gravity, climbing, three NPCs, stars. Outcomes are hardcoded — the model arrives in Layer 3.

Every number, type and algorithm is specified. Nothing to fill in. If AI Studio deviates, quote the relevant section back at it rather than re-describing.

Rationale: `word-lab-world-design.md` · tiers: `word-lab-age-tiers-6-to-12-design.md`

```text
Build "Word Lab", a 2D side-view browser game for children aged 6-12
learning English. React + TypeScript + Tailwind, in Google AI Studio.
This layer is the world and local state only: no Firebase, no model
call, no routing.

================ WHAT KIND OF GAME THIS IS ================

Like Scribblenauts. The child walks a character through a side-view
level, meets people who need something, and SUMMONS the thing by writing
its name in English. The object drops into the world and STAYS there.

THE RULE THAT MAKES THE GAME WORK:
  THE AVATAR CANNOT JUMP. Height must be summoned.
To reach the roof the child needs something TALL and RIGID - a ladder, a
tree. A rope is tall but not rigid, so it will not do. The English
property word IS the traversal system. Do not add a jump key.

================ ARCHITECTURE - DECIDED, DO NOT SUBSTITUTE ================

RENDERING: absolutely-positioned DOM elements inside one <div id="world">.
No <canvas>. Each sprite is an <img> positioned with
`transform: translate3d(Xpx, Ypx, 0)`. Reason: keyboard focus,
screen readers and text all work, and React handles it reliably.

THE LOOP: one requestAnimationFrame loop. Delta time in seconds, clamped
to a maximum of 0.032.

STATE SPLIT - this is the most important architectural rule:
- ALL moving game state lives in a single useRef object and is mutated
  directly in the loop. Avatar position, object positions, velocities.
- React useState is ONLY for UI that changes rarely: notepad open/closed,
  the current verdict sentence, star count, which NPC bubble is showing.
- The loop writes positions by setting element.style.transform directly
  through refs. It must NEVER call setState per frame.
If you re-render React 60 times a second this game will stutter on a
tablet. Do not do it.

SCALING: the world renders at a fixed 1280x720 and is scaled to fit the
browser with a CSS transform on a wrapper, preserving aspect ratio,
letterboxed. Same approach as a slide deck.

================ UNITS AND CONSTANTS ================

World pixels = CSS pixels. Origin top-left, +y is DOWN.

const LEVEL_W = 2400;      // total level width
const LEVEL_H = 720;
const VIEW_W  = 1280;      // camera viewport
const GROUND_Y = 620;      // the ground surface line
const GRAVITY = 1800;      // px/s^2
const MAX_FALL = 1200;     // px/s
const WALK_SPEED = 160;    // px/s
const CLIMB_SPEED = 90;    // px/s
const CAMERA_LERP = 0.12;  // per frame, toward target
const PICKUP_RANGE = 60;   // px, horizontal
const GIVE_RANGE = 70;     // px, horizontal
const CLIMB_SNAP_X = 60;   // px, horizontal tolerance at platform edge
const CLIMB_SNAP_Y = 40;   // px, vertical tolerance at platform edge

Sprite anchoring: every object and character has its origin at
BOTTOM-CENTRE. An entity standing on the ground has y === GROUND_Y.

================ LEVEL GEOMETRY - EXACT ================

One hand-drawn level, 2400 x 720, laid out left to right:
- x 0-880:      street, with a lamp post at x=420 whose top is y=300
- x 900-1700:   a building, interior visible in cross-section
                  ground floor = a small cafe, floor at GROUND_Y
                  upper floor,  floor top at y=380
- x 880-1720:   the roof, floor top at y=180
- x 1720-2400:  street continues, a tree stump and a bench (decor only)

PLATFORMS - solid surfaces the avatar can stand on:
const PLATFORMS = [
  { x1: 0,    x2: 2400, top: 620 },   // the ground
  { x1: 900,  x2: 1700, top: 380 },   // the upper floor
  { x1: 880,  x2: 1720, top: 180 },   // the roof
];

The avatar spawns at x=120, y=GROUND_Y, facing right.

Note the vertical gaps: ground 620 -> upper floor 380 is 240px; ground
-> roof is 440px. Nothing in the level lets you climb them. That is
deliberate: the only way up is a summoned climbable object.

================ TYPES - USE THESE EXACT SHAPES ================

Layers 3 and 4 depend on these. Do not rename fields.

type PropertyId =
  | 'big' | 'small' | 'hot' | 'cold' | 'wet' | 'dry'
  | 'soft' | 'hard' | 'heavy' | 'loud'
  | 'long' | 'short' | 'tall' | 'rigid' | 'flexible'
  | 'floats' | 'sinks' | 'sharp' | 'hollow' | 'round'
  | 'transparent' | 'opaque' | 'conducts electricity' | 'insulates'
  | 'magnetic' | 'absorbent' | 'waterproof' | 'heat-resistant'
  | 'gives light' | 'stretchy';

type Verdict = 'accept' | 'reject' | 'unknown';
type SizeClass = 'small' | 'medium' | 'tall';   // 64 | 120 | 460 px high

interface Judgement {
  word: string;
  verdict: Verdict;
  properties: PropertyId[];
  sentence: string;
  size: SizeClass;
  sprite: string | null;   // asset key, or null -> render a labelled shape
}

interface WorldObject {
  id: string;
  word: string;
  x: number; y: number;    // bottom-centre
  vy: number;
  w: number; h: number;
  sprite: string | null;   // null -> labelled shape (Layer 2 uses this)
  properties: PropertyId[];
  climbable: boolean;      // derived: has BOTH 'tall' and 'rigid'
  grounded: boolean;
  carriedBy: 'avatar' | null;
}

interface Npc {
  id: string;
  x: number; y: number;
  wants: PropertyId[];
  line: string;            // shown in the speech bubble
  satisfied: boolean;
  sprite: string;
}

interface Avatar {
  x: number; y: number;
  vy: number;
  facing: 1 | -1;
  climbing: boolean;
  carryingId: string | null;
}

================ THE THREE NPCs ================

const NPCS: Npc[] = [
  { id:'roof',   x:1550, y:180, wants:['tall','rigid'],
    line:"I am stuck up here! I need something TALL and RIGID to climb down.",
    satisfied:false, sprite:'npc-roof' },
  { id:'cafe',   x:1100, y:620, wants:['hot'],
    line:"I am freezing. Bring me something HOT.",
    satisfied:false, sprite:'npc-cafe' },
  { id:'street', x:460,  y:620, wants:['long'],
    line:"My balloon is stuck on the lamp. I need something LONG to reach it.",
    satisfied:false, sprite:'npc-street' },
];

The property words inside `line` render as chips: --chip-bg, --chip-text,
bold, --radius-sm. The want IS the puzzle. There is no separate puzzle
screen; the world is the interface.

================ SYSTEMS - EXACT ALGORITHMS ================

--- 1. INPUT ---
Left/Right or A/D, or press-and-hold the left or right third of the
screen on touch: set avatar.vx intent. Touch walk zones must NOT cover
any UI element - a tap that lands on the notepad button, the star
counter or a bubble goes to that control, never to walking.
Up/Down or W/S: climb, only inside a climb zone (below).
N: open the notepad. E: pick up / drop. Enter: give, when in range.
While the notepad is open, all movement input is ignored.

--- 2. GRAVITY AND LANDING (avatar and objects, same function) ---
if (!climbing && !carried) {
  vy = Math.min(vy + GRAVITY * dt, MAX_FALL);
  const nextY = y + vy * dt;
  const surface = highestPlatformBetween(y, nextY, x);
  if (surface !== null) { y = surface; vy = 0; grounded = true; }
  else { y = nextY; grounded = false; }
}
highestPlatformBetween(yFrom, yTo, x): among PLATFORMS where
x1 <= x <= x2 and yFrom <= top <= yTo, return the smallest `top`.
Returns null if none. This is downward-only collision - an entity moving
up passes through platforms. That is intended and keeps climbing simple.

--- 3. NO OBJECT-TO-OBJECT COLLISION ---
Objects never collide with each other. They may overlap. Do not add
stacking, pushing, or rotation. This is a hard scope limit.

--- 3b. NO WALL COLLISION ---
The avatar walks freely through the building's walls. The building is
drawn in cross-section, like a doll's house, so walking "into" the cafe
is correct. Only PLATFORMS stop movement, and only downward. Do not add
vertical wall collision.

--- 4. CLIMBING - a zone, not physics ---
A WorldObject with climbable === true and grounded === true creates a
climb zone: the rect
  x from (obj.x - 30) to (obj.x + 30),
  y from obj.y (its base) up to Math.max(obj.y - obj.h, 0) (its top,
  clamped so the avatar can never climb above the level).
While the avatar's x is inside that range AND the avatar's y is within
the zone's vertical span:
  - gravity is disabled for the avatar
  - Up moves avatar.y up by CLIMB_SPEED * dt, clamped to the zone top
  - Down moves it down, clamped to the zone base
On leaving the top of the zone, snap onto a platform if one has
  |platform.top - avatar.y| <= CLIMB_SNAP_Y and
  platform.x1 - CLIMB_SNAP_X <= avatar.x <= platform.x2 + CLIMB_SNAP_X
If so, set avatar.y = platform.top and climbing = false.
Stepping off a platform edge simply re-enables gravity; the avatar falls.

--- 5. SUMMONING ---
When a word resolves to accept or reject, create a WorldObject at
  x = avatar.x + 80 * avatar.facing
  y = Math.max(40, avatar.y - 300)     // 300px above the avatar's feet
  vy = 0
so it visibly falls in from above, wherever the avatar is standing.
Do NOT use a fixed spawn height: if the avatar is on the roof, an object
spawned at a fixed y=200 would appear below their feet. Height from SizeClass: small 64, medium 120,
tall 460. Width = height for small and medium; tall objects are 120 wide.
climbable = properties includes BOTH 'tall' and 'rigid'.
A puff-of-smoke sprite plays at the spawn point for 300ms.

REJECTED WORDS STILL SUMMON. The object appears, falls, lands and stays.
It simply lacks the property. A rope lands in a floppy heap. The child
must see that their word made something real. Only 'unknown' summons
nothing.

Objects are NEVER removed. A level littered with a child's past attempts
is the point, not a leak.

--- 6. CARRYING ---
Press E when |avatar.x - obj.x| <= PICKUP_RANGE and the object is
grounded and nothing is carried: set carriedBy='avatar'. While carried,
the object renders at (avatar.x, avatar.y - 76) - above the head - and
skips gravity. Press E again to drop: carriedBy=null, vy=0, gravity
resumes from where it is.

--- 7. GIVING AND STARS ---
Press Enter when carrying an object and |avatar.x - npc.x| <= GIVE_RANGE
and |avatar.y - npc.y| <= 80. If the object's properties include EVERY
id in npc.wants: the NPC becomes satisfied, the object is removed, a
star sprite spins from the NPC to a counter in the top-left, stars += 1.
Otherwise the NPC shakes their head once and nothing else happens - no
penalty, no message about the child.

The roof NPC is special: satisfying them does not need carrying. Climb
up, walk within GIVE_RANGE, and they stand up and follow you down.

Stars are capped at 3. At stars === 3, show a LEVEL COMPLETE panel:
--color-paper background, --outline, one button "PLAY AGAIN". No score,
no rating, no timer, no stars-out-of-three.

PLAY AGAIN resets: objects = [], every npc.satisfied = false, stars = 0,
avatar back to x=120, y=GROUND_Y, carryingId = null, camera to 0. It does
NOT clear the word shelf - words the child has learned are theirs to
keep, and in Layer 3 that shelf becomes persistent.

--- 8. CAMERA ---
targetX = clamp(avatar.x - VIEW_W/2, 0, LEVEL_W - VIEW_W)
cameraX += (targetX - cameraX) * CAMERA_LERP
Apply as `transform: translate3d(${-cameraX}px, 0, 0)` on #world.
Vertical never moves - the whole 720px height is always visible.

UI LIVES OUTSIDE #world. The notepad button, the star counter, the
outcome bubble, the level-complete panel and the mode switcher are
siblings of #world, positioned against the 1280x720 viewport. If you put
them inside #world they will slide away with the camera.
Speech bubbles above NPCs DO live inside #world - they belong to the
scene and should move with it.

--- 9. THE ACTIVE GATE ---
The notepad needs to know which NPC's `wants` it is judging against.
activeGate = the NPC whose speech bubble was shown most recently and who
is not yet satisfied. If none has been shown, use the nearest unsatisfied
NPC by |avatar.x - npc.x|.
Show the active NPC's name or icon at the top of the notepad so the child
knows who they are helping. If every NPC is satisfied, the notepad still
opens and everything summons, judged against an empty gate - free play.

================ DESIGN TOKENS ================

Put these in index.css under :root and register them in the Tailwind
theme so every utility class resolves to a token. No raw hex and no
arbitrary values anywhere in the markup: no bg-[#...], no p-[13px].
Write DESIGN.md to the project root with this token set plus the DON'T
list below, and re-read it before every later change I ask for.

:root{
  --color-sky:#A8DCF0;        --color-ground:#7EC850;
  --color-ink:#1A1A1A;        --outline-w:3px;
  --outline:var(--outline-w) solid var(--color-ink);
  --color-paper:#FFF8E7;      --color-paper-2:#F2E7CE;
  --color-accent:#C43F10;     --color-on-accent:#FFFFFF;
  --color-star:#FFC629;
  --color-success:#157F4B;    --color-warning:#8A5200;

  --font-stack:"Atkinson Hyperlegible","Verdana",system-ui,sans-serif;
  --font-weight-regular:400;  --font-weight-bold:700;
  --text-display:34px;   --lh-display:1.2;
  --text-title:26px;     --lh-title:1.25;
  --text-subtitle:20px;  --lh-subtitle:1.35;
  --text-body:18px;      --lh-body:1.6;
  --text-small:16px;     --lh-small:1.5;
  --measure-max:42ch;

  --space-1:8px;  --space-2:16px; --space-3:24px;
  --space-4:32px; --space-5:48px; --space-6:64px;

  --radius-sm:8px; --radius:14px; --radius-lg:22px; --radius-circle:50%;
  --shadow-ground:0 4px 0 rgba(26,26,26,.18);   /* the only shadow */

  --touch-min:56px;   --motion:200ms cubic-bezier(.2,.8,.2,1);
  --reading-max-words:25;  --reading-cefr:"A2";

  --bubble-bg:var(--color-paper);   --bubble-border:var(--outline);
  --notepad-bg:var(--color-paper);  --notepad-border:var(--outline);
  --chip-bg:var(--color-paper-2);   --chip-text:var(--color-ink);
  --verdict-accept:var(--color-success);
  --verdict-reject:var(--color-warning);
  --focus-ring:3px solid var(--color-accent);
}

Contrast is already computed and all pairs pass WCAG AA. Do not change
these colours: ink on paper 16.4:1, ink on sky 11.7:1, accent on paper
4.9:1, white on accent 5.2:1.

================ THE NOTEPAD ================

A button fixed to the top-right of the viewport, at least --touch-min,
drawn as a small paper notepad with --outline. Pressing it or N opens a
panel over the world: --notepad-bg, --notepad-border, --radius-lg,
max-width 520px, centred. The world stays visible behind it.

Build all THREE input modes now as one component with a `mode` prop.
Do not build three screens - retrofitting this later means rewriting the
input. Default mode for this layer: WRITE.

WRITE: one text input at least --touch-min tall, placeholder
  "write a word in English", plus a button --touch-min tall: "MAKE IT".

BUILD: the same input, plus 12 word chips above it, each at least
  --touch-min tall. Tapping a chip fills the input; it does NOT submit.
  Six of the twelve satisfy the activeGate and six do not. A bank of only
  correct answers turns it into multiple choice and the child stops
  reading. Chips are text only - no art needed.

  const BUILD_BANK = {
    roof:   { ok:['ladder','tree','stairs','slide','pole','lamppost'],
              no:['rope','ribbon','snake','balloon','cloud','feather'] },
    cafe:   { ok:['soup','fire','tea','candle','heater','oven'],
              no:['ice','snow','fan','water','stone','glass'] },
    street: { ok:['stick','broom','pole','rope','arm','ribbon'],
              no:['coin','cup','shoe','hat','button','ring'] },
  };

  Every `ok` word must actually satisfy that NPC's gate under the
  CATALOGUE below, and every `no` word must actually fail it. Verify this
  in code with an assertion at startup - if the bank and the catalogue
  ever disagree, the game is teaching the child something false.

  Note `rope` appears as WRONG for the roof and RIGHT for the street. A
  rope is long but not rigid. The same word behaving differently at
  different gates is the lesson, not a bug - keep it. `broom` and `pole`
  do the same in reverse.

PICK: no text input. Six picture cards, each at least 96x96, each
  showing the object with its English word underneath at --text-body.
  Tapping a card submits immediately - a six-year-old should not have to
  find a second button. Two of the six satisfy the gate. Every card word
  must have a real sprite, so use exactly these sets:

  const PICK_CARDS = {
    roof:   ['ladder','tree','rope','balloon','coin','ice'],      // ok: ladder, tree
    cafe:   ['soup','fire','ice','balloon','coin','rope'],        // ok: soup, fire
    street: ['stick','broom','coin','balloon','ice','soup'],      // ok: stick, broom
  };

Add a dev-only mode switcher in the corner so I can test all three.

Switching mode must never move the world, the camera or the NPCs.

READ-ALOUD: a button on every speech bubble and every outcome sentence
using window.speechSynthesis. No audio files, no API key. Silent unless
pressed.

================ THE LOCAL CATALOGUE FOR THIS LAYER ================

Layer 2 replaces this with a model call producing the same Judgement
shape. Until then, judge locally.

Do NOT write a word -> sentence table. A word's verdict depends on which
gate it is judged against - `rope` fails ['tall','rigid'] and passes
['long'] - so a flat sentence table cannot be correct. Store PROPERTIES
and generate the sentence.

const CATALOGUE: Record<string,{p:PropertyId[]; size:SizeClass; sprite:string|null}> = {
  ladder:{p:['tall','rigid'],size:'tall',sprite:'ladder'},
  tree:{p:['tall','rigid','hard'],size:'tall',sprite:'tree'},
  stairs:{p:['tall','rigid','hard'],size:'tall',sprite:'stairs'},
  slide:{p:['tall','rigid','hard'],size:'tall',sprite:null},
  pole:{p:['tall','long','rigid'],size:'tall',sprite:null},
  lamppost:{p:['tall','rigid','hard'],size:'tall',sprite:null},
  broom:{p:['long','rigid'],size:'tall',sprite:'broom'},
  stick:{p:['long','rigid','hard'],size:'medium',sprite:'stick'},
  arm:{p:['long','flexible'],size:'medium',sprite:null},
  rope:{p:['tall','long','flexible'],size:'tall',sprite:'rope'},
  ribbon:{p:['long','flexible','soft'],size:'small',sprite:null},
  snake:{p:['long','flexible'],size:'medium',sprite:null},
  soup:{p:['hot','wet'],size:'small',sprite:'soup'},
  tea:{p:['hot','wet'],size:'small',sprite:null},
  fire:{p:['hot','gives light'],size:'medium',sprite:'fire'},
  candle:{p:['hot','gives light','small'],size:'small',sprite:null},
  heater:{p:['hot','hard'],size:'medium',sprite:null},
  oven:{p:['hot','hard','big'],size:'medium',sprite:null},
  ice:{p:['cold','hard','small'],size:'small',sprite:'ice'},
  snow:{p:['cold','soft','wet'],size:'small',sprite:null},
  fan:{p:['cold','hard'],size:'medium',sprite:null},
  water:{p:['wet','cold'],size:'small',sprite:null},
  stone:{p:['hard','heavy','small'],size:'small',sprite:null},
  glass:{p:['transparent','hard'],size:'small',sprite:null},
  balloon:{p:['round','soft','big'],size:'small',sprite:'balloon'},
  cloud:{p:['soft','big'],size:'medium',sprite:null},
  feather:{p:['soft','small'],size:'small',sprite:null},
  coin:{p:['small','hard','round'],size:'small',sprite:'coin'},
  cup:{p:['small','hollow','hard'],size:'small',sprite:null},
  shoe:{p:['small','soft'],size:'small',sprite:null},
  hat:{p:['small','soft'],size:'small',sprite:null},
  button:{p:['small','hard','round'],size:'small',sprite:null},
  ring:{p:['small','hard','round'],size:'small',sprite:null},
  jetpack:{p:['heavy','hard'],size:'medium',sprite:'jetpack'},
};

Every word in BUILD_BANK and PICK_CARDS is in this catalogue. That is a
requirement, not a coincidence: a child who taps a chip and is told "I
do not know that word" has been lied to by the interface.

JUDGE LOCALLY:
  const entry = CATALOGUE[word.trim().toLowerCase()];
  if (!entry) -> verdict 'unknown', summon nothing,
                 sentence "I do not know that word. Try another one."
  const missing = gate.wants.filter(w => !entry.p.includes(w));
  verdict = missing.length === 0 ? 'accept' : 'reject';

SENTENCE TEMPLATES - plain, and Layer 2 will do better:
  accept: `A ${word} is ${list(gate.wants)}, so it works.`
  reject: `A ${word} is ${list(entry.p ∩ gate.wants)}, but it is not
           ${list(missing)}.`
          If the intersection is empty:
           `A ${word} is not ${list(missing)}.`
  list() joins with " and ": ['tall','rigid'] -> "tall and rigid".
Sentences never mention the child. No "good job", no "try again".

LABELLED SHAPES - build this now, not in Layer 2.
When sprite is null, render the object as a rounded rectangle at its
SizeClass dimensions: --color-paper-2 fill, --outline border,
--radius-sm, with the English word centred on it in --font-stack bold at
--text-body, --color-ink, wrapped to fit the box.
This is instant, matches the art style, and printing the word on the
object reinforces the spelling. A child summoning `snake` gets a boxy
thing that says SNAKE, and that is honest and charming. Never show a
loading spinner in the world; never call an image model at runtime.

Outcome sentence display: in a bubble under the notepad, --verdict-accept
for accept and --verdict-reject for reject. On reject the notepad
reopens with the field cleared and focused so the child retries at once.
This is the most important moment in the game: it must never feel like
being marked wrong. No red, no cross, no buzzer, no counter, no shake.

================ ART TO GENERATE ================

One consistent hand-drawn style throughout: thick black outlines about
3px and slightly wobbly as if drawn with a marker, flat saturated fills,
no gradients, no glows, no baked-in shadows. Characters have round
heads, big simple eyes, minimal mouths, chunky limbs, readable at
thumbnail size.

Generate, all PNG with transparent backgrounds except the background:
- background.png, 2400x720, ONE image containing sky, ground, street,
  lamp post at x=420, the building at x=900-1700 in cross-section with
  a cafe below and a room above, the roof, and the decor at x>1720.
  The visual floor lines MUST sit at y=620, y=380 and y=180 to match
  PLATFORMS exactly.
- avatar-1/2/3.png, 48x72, three walk frames
- npc-roof.png, npc-cafe.png, npc-street.png, 48x72 each
- Objects at their size class, transparent, standing on their bottom
  edge: ladder 120x460, tree 120x460, stairs 120x460, broom 120x460,
  rope 120x460 (drawn slack and floppy), fire 120x120, stick 120x120,
  jetpack 120x120, soup 64x64, ice 64x64, balloon 64x64, coin 64x64
- puff.png, 120x120, a smoke puff
- star.png, 64x64

No grey placeholder boxes anywhere.

================ DON'T ================

1. No gradients, no bevels, no glows, no shadow except --shadow-ground.
2. No flat corporate vector look - the outline must wobble.
3. A rejected word never uses red. Rejection is --verdict-reject amber.
4. No score, no percentage, no accuracy, no report card, no timer.
5. No pill geometry, no mascot narrator, no confetti on every success.
6. No jump key. No object-to-object collision. No procedural level.

================ ACCESSIBILITY ================

- --focus-ring on every focusable element.
- The whole level completable on keyboard alone: arrows to walk, N for
  the notepad, type, Enter to summon, E to pick up and drop, Up/Down to
  climb, Enter to give.
- Tap targets at least --touch-min. All text at least --text-small.
- The verdict must be readable without colour: the sentence says what
  happened; colour only reinforces it.

================ SELF-CHECK BEFORE YOU FINISH ================

Verify each of these yourself and tell me any that fail:
1. Walking from x=120 to x=2280 pans the camera and stops at both edges.
   The notepad button and star counter do NOT move while it pans.
2. Summoning `ladder` near x=1500 drops a 460px object that lands with
   its base at y=620.
3. Standing at that ladder and holding Up raises the avatar to y=180 and
   snaps them onto the roof platform.
4. Walking off the roof edge makes the avatar fall and land at y=620.
5. Summoning `rope` also produces an object that lands and stays, and it
   is NOT climbable.
6. Summoning `florb` produces no object.
7. Summoning `snake` produces a labelled box reading SNAKE, not a
   missing-image icon.
8. Carrying `soup` to the cafe NPC awards a star; carrying `ice` there
   does not, and shows no penalty.
9. `rope` REJECTS at the roof NPC and ACCEPTS at the street NPC. Same
   word, two gates, two answers.
10. A startup assertion confirms every BUILD_BANK.ok word satisfies its
    gate and every .no word fails it, against CATALOGUE. It should pass
    silently; if it throws, the bank and the catalogue disagree.
11. BUILD mode shows 12 chips, PICK mode shows 6 cards, and every card
    word has a real sprite.
12. Summoning while standing on the roof drops the object from above the
    roof, not below it.
13. React does not re-render during movement - confirm the loop mutates
    refs and sets style.transform directly, and never calls setState per
    frame.

Output complete working code. No placeholders, no "add logic here".
```

## Sau khi build xong — kiểm tra theo đúng thứ tự này

1. Đi trái phải hết màn. Camera phải trượt mượt và **dừng ở hai mép**, không lòi ra ngoài.
2. Mở sổ, gọi `ladder`. Nó phải **rơi xuống, chạm đất, và nằm lại đó**.
3. Đứng vào thang, giữ Up → lên mái. Đi ra mép mái → rơi xuống đất.
4. Gọi `rope`. **Phải hiện ra và nằm lại**, mềm oặt, không leo được. Nếu không hiện gì thì đó là lỗi phải sửa đầu tiên — bé cần thấy chữ mình viết tạo ra vật thật.
5. Gọi `florb` → không có gì.
6. Vác `soup` tới NPC quán cà phê → được sao. Vác `ice` tới → lắc đầu, **không có gì mang tính phạt**.
7. Chơi hết màn chỉ bằng bàn phím.
8. Mở DevTools → React DevTools → bật "Highlight updates". **Khi đi lại không được có ô nhấp nháy.** Có là loop đang setState mỗi frame, phải sửa ngay trước khi qua Layer 2.

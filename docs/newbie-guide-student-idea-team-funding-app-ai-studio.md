# Newbie Guide: Build "Ươm Mầm" — a Student Idea → Team → Funding App

Build a **web app + Android app** where students share project ideas, form teams, and gather community support — using Google AI Studio, with no coding experience.

Target reader: complete beginner. Estimated time: **3–5 hours** for a working, published web app. Add ~2 hours for Android.

Sources this guide follows: `Handbook_airiser_2026.pdf` (official AI Riser participant handbook), `Vibe_Coding_Handbook.pptx` (goo.gle/itsvibecoding, 47 slides).

---

## 0. What you are building

**Ươm Mầm** — "nurturing seeds".

The loop:

1. A student posts an idea (even a rough one).
2. Other students browse ideas and ask to join.
3. A team forms and posts progress updates.
4. When ready, the team opens a **support campaign** — the community pledges money, materials, mentoring, or time.

Four screens. That's the whole MVP:

| Screen | Purpose |
|---|---|
| Bảng ý tưởng | Browse/filter idea cards |
| Chi tiết ý tưởng | Full idea + team + "Xin tham gia" |
| Đội của tôi | My teams + shared update thread |
| Chiến dịch ủng hộ | Campaign with goal + pledge list |

---

## 1. Read this before you build anything

Your users include **6-year-olds**. That single fact changes the design, and getting it wrong builds something genuinely harmful. Two rules are non-negotiable.

### Rule 1 — Age tiers, not one app for everyone

A 6-year-old and a 20-year-old cannot have the same account capabilities.

| Age band | Can do | Cannot do |
|---|---|---|
| **6–12** "Lớp học" | Join with a **class code** from a teacher. See only their class's ideas. Post ideas to the class. | No public profile, no photos, no messaging, no campaigns |
| **13–15** | Post ideas publicly after moderation. Join teams. | No private messages. No campaigns. |
| **16–17** | Public ideas, teams, create a campaign | Campaign marked "cần người giám hộ xác nhận" |
| **18+** | Everything | — |

**Never allow private one-to-one messaging between different age bands.** All team discussion happens in a team thread that is visible to the whole team. For teams containing under-16s, a supervising adult (teacher) is a member of that thread. This one design choice removes the single largest risk in a platform that connects minors with strangers.

Also: no precise location, no phone numbers, no email addresses in public posts, and never a face photo combined with a school name. Your AI moderation step (built below) enforces this automatically.

### Rule 2 — Do not build payments

This is the most important engineering advice in this guide, and it's the opposite of what most people assume.

Your campaign feature handles **pledges, not transactions.** A pledge is a promise — of money, materials, mentoring, or hours. Fulfilment happens off-platform: through the school's account, an existing licensed platform, or in person.

Why this is right, not a cop-out:

- **Legal.** Minors cannot enter binding contracts. A child receiving public money creates obligations they can't hold. Handling other people's money means KYC, payment licensing, and refund liability — none of which a student MVP can carry.
- **Practical.** Payment integration is the fastest way for a beginner MVP to stall. You'll spend your entire build budget on it and have no product to show.
- **It demos identically.** A judge or user sees the same complete loop: campaign → goal → pledges → progress. Nothing is missing from the story.

If the project later needs real money, route it through a licensed provider with **the school or a guardian as merchant of record** — never the child.

Write both rules into your submission text. Deliberate, explained scope limits read as maturity, not as gaps.

---

## 2. Setup (15 minutes)

1. **Get a fresh Google account** — or use one that has *never published an app* from AI Studio. This unlocks **Starter Tier**: publish free, **no credit card, no Google Cloud project**. Up to 2 apps, single region. If you get asked for a credit card during publishing, you are not on Starter Tier — try incognito with a clean account.
2. Open **https://ai.dev** → sign in → left panel → **Build** → **+ New app**.
3. Optional, for later: **Antigravity** (agentic IDE) at `antigravity.google/download`. You do not need it for this guide.

---

## 3. Step 1 — Sharpen your prompt first

The official handbook's method: refine the prompt with Gemini *before* pasting into AI Studio.

Go to https://gemini.google.com and say:

```
Please prepare a prompt for me to send to Google AI Studio to vibe-code this app:
a platform where students aged 6-22 share project ideas, form teams, and collect
community pledges. Different age groups must have different permissions for safety.
```

A weak prompt gets a weak app. The handbook's anatomy of a strong prompt has six layers:

| Layer | Example |
|---|---|
| Role | "You are an expert full-stack developer and UX/UI designer…" |
| Goal | "Build a platform where students share ideas and form teams" |
| Context | "Users are 6–22 years old, mostly on phones, in Vietnam" |
| Does it need AI? | "Use Gemini to structure rough ideas and moderate posts" |
| The vibe | "Bright, friendly, like a school project fair" |
| Visual (optional) | Attach a sketch or screenshot |

I've done this for you below. Read it, then change it to match *your* vision — the handbook's Pro tip #1 exists because copying blindly gives you someone else's app.

---

## 4. Step 2 — The master prompt (copy this)

Paste into AI Studio Build and click **Build**.

```
System Role: You are an expert full-stack developer and UX/UI designer who builds
safe, accessible products for children and teenagers.

Task: Build a complete, working web application called "Ươm Mầm" — a platform where
students aged 6 to 22 share project ideas, form teams, and gather community support.

Tech Stack: React single-page app, Tailwind CSS, mobile-first responsive.

THE MOST IMPORTANT RULE — AGE TIERS.
On first open the user picks an age band. This choice controls what they can do:
- 6-12 ("Lớp học"): joins with a class code. No public profile, no photos, no
  messaging, no campaigns. Sees only ideas sharing their class code.
- 13-15: can post ideas publicly after moderation. Can join teams. No private
  messages. No campaigns.
- 16-17: public ideas, teams, and campaigns, but every campaign displays the badge
  "Cần người giám hộ xác nhận".
- 18+: all features.
Never allow private one-to-one messaging between different age bands. All team
discussion happens in one shared team thread visible to every team member.

Core screens (exactly four):
1. Bảng ý tưởng — grid of idea cards, filter by category and age band
2. Chi tiết ý tưởng — full idea, team members, "Xin tham gia" button
3. Đội của tôi — teams I own or joined, with a shared update thread
4. Chiến dịch ủng hộ — campaign page with a goal and a list of pledges

IMPORTANT: campaigns collect PLEDGES, not payments. A pledge is a promise of money,
materials, mentoring, or hours. There is no checkout, no card form, no payment
processing anywhere in this app. Show pledge progress toward the goal.

AI features (use Gemini):
- "Trợ lý ý tưởng": the user types a rough idea in any wording. Gemini returns a
  structured card (Vấn đề / Ai gặp vấn đề này / Giải pháp / Bước đầu tiên) and asks
  3 short questions to sharpen it.
- "Đọc theo tuổi": a toggle that rewrites any idea description at the reader's
  reading level — simple words for a 7-year-old, normal language for a teenager.
- "Đội cần ai": from an idea, suggest the 3 roles the team needs.
- "Kiểm duyệt": before any idea or comment is published, Gemini checks it for
  personal contact details, unsafe content, or bullying, and blocks it with a
  friendly explanation of what to change.

Data: use browser localStorage. Seed the app with 8 sample ideas across different
age bands and categories so it is never empty on first open.

Accessibility (required):
- Every action reachable by keyboard
- WCAG AA colour contrast
- Large tap targets, usable one-handed on a phone
- Alt text on every image
- Every progress bar also shows its value as text

The Vibe: bright, friendly, encouraging. Rounded cards, warm colours, generous
whitespace. It should feel like a school project fair, not a corporate dashboard.
UI language: Vietnamese.

Output: complete working code. No placeholders, no "// add logic here".
```

**Why this prompt is long:** the handbook's Pro tip is that sophistication in equals quality out. Notice that the safety rules are *inside* the prompt — you are not bolting safety on afterwards, you are making the AI build it in from the first render.

---

## 5. Step 3 — Iterate in layers

The Vibe Coding Handbook calls this the **Layered Build Approach**: core logic first, then aesthetics, then AI features. Do not ask for everything at once.

Send these one at a time, testing after each.

**Layer 1 — the join flow**
```
Add the "Xin tham gia" flow: a student sends a short message asking to join, the
idea owner sees pending requests and can accept or decline. Accepted members appear
on the idea's team list. Respect the age rules already defined.
```

**Layer 2 — team updates**
```
In "Đội của tôi", add a shared update thread where any team member can post a short
progress update with an optional image. Show updates newest first with the author's
display name and age band. No private messages anywhere.
```

**Layer 3 — the campaign**
```
Add campaign creation for teams. A campaign has: a title, the story, what the team
needs, a goal, and a deadline. Supporters submit a pledge choosing a type — Tiền,
Vật liệu, Cố vấn, or Thời gian — with an amount or description and their name.
Show progress toward the goal. Remember: pledges only, no payment form.
```

**Layer 4 — the AI coach**
```
Improve "Trợ lý ý tưởng": after the user answers the 3 questions, regenerate a
polished idea card and let them publish it in one click. Keep the language simple
enough for a 10-year-old to understand.
```

**Layer 5 — moderation you can see**
```
Make the moderation step visible: when a post is blocked, show a friendly panel
explaining exactly which rule it broke and how to fix it. Add a small shield icon
on every published idea meaning "đã kiểm duyệt".
```

**Layer 6 — accessibility pass**
```
Do a full accessibility pass: keyboard navigation for every interactive element,
visible focus rings, ARIA labels, WCAG AA contrast, and a text equivalent for every
progress bar and chart. List what you changed.
```

### Three techniques worth knowing

- **Fix button** — when you hit an error, click **Fix** and let Gemini self-heal. Don't debug by hand.
- **Annotate** — click "Annotate app", draw on the part you want changed, describe the change. Far faster than describing a UI element in words.
- **The Architect Interview** — before a big feature, ask: *"I want to add X. Ask me 5 technical questions about the user flow before you start coding."* This catches mismatches before they become code.

---

## 6. Step 4 — Google integrations (worth +10 points)

The handbook awards **up to 10 extra points** for integrating Google technologies. Pick integrations that genuinely fit — bolted-on tech is obvious to judges.

| Integration | Use it for | Effort |
|---|---|---|
| **Gemini** | Already core — coach, age-adaptive reading, moderation | Done |
| **Firebase Auth** | "Đăng nhập bằng Google" so teams persist across devices | Low |
| **Firestore** | Replace localStorage so ideas are shared between real users | Medium |
| **Google Sheets** | Teacher exports class ideas; a class roster becomes your class-code source | Low |
| **Google Calendar** | Team meeting scheduling from the team thread | Low |
| **Maps** | Show local ideas — **only at district level, never precise location** for minors | Low |

In AI Studio, select the integration chip **below the prompt box before clicking Build** so it knows the integration is required, then approve the permission prompt ("Let's do it").

Suggested prompt:

```
Add Firebase Authentication with "Đăng nhập bằng Google" and move idea, team, and
pledge storage from localStorage to Firestore, so different users on different
devices see the same ideas. Keep all the age-band rules enforced on read and write.
```

**Important:** localStorage → Firestore is the moment your app becomes multi-user, and it is also the moment your safety rules start mattering for real. Re-test every age tier after this change.

---

## 7. Step 5 — Publish the web app (free)

The handbook: publishing is optional but earns **+10 points**.

1. Top right → **Publish** → **Get started**.
2. Set the description and app URL.
3. **Publish your app** → you get a public `https://your-app.ai.studio` URL.

Anyone with the link can use the app without seeing your code or prompts.

**If it asks for a credit card**, you are not on Starter Tier. Fix: use a Google account that has never published an AI Studio app, or try incognito. Starter Tier gives you 2 apps free with no Cloud project and no billing.

---

## 8. Step 6 — The Android app

AI Studio can build Android apps too, but understand the cost before you start.

1. In your app, top right → **Publish**.
2. **Get started** → "Publish your app to test on Play Console".
3. **Create account** → a Play Console developer account costs a **one-time USD 25** fee.
4. Choose "Yourself" unless you have a registered business.
5. Wait **a few business days** for account review.
6. Once reviewed → **Publish app for testing** → you get a Play link testers can install from.

Two honest caveats:

- This is a **test track**, not a public Play Store listing. The handbook notes full Play Store publishing is "coming soon" and that the app remains unverified — it's for testers, not the general public.
- The **$25 + multi-day review** means you cannot decide to do this the night before a deadline. If you want the Android app, start the account today and build the web app while it's in review.

**My recommendation for a beginner:** ship the web app first and publish it. It's free, instant, works on every phone through the browser, and earns the same +10. Treat Android as a stretch goal.

---

## 9. Step 7 — Submitting to AI Riser Vietnam 2026

Deadline: **30 Aug 2026**. Form: `goo.gle/airiservietnam-completion`

| Item | Required? | How |
|---|---|---|
| **AI Studio project link** | **Mandatory** | Share (top right) → access **Public** → Copy link. Judges use this to see your project. |
| Deployed app link | Optional, **+10** | The `.ai.studio` URL from Step 5 |
| Google tech integration | Optional, **+10** | Firebase / Sheets / Maps / Workspace |
| Category | Yes | "Education" or "Inclusive access" both fit |

Judging is Feasibility 40% / Impact 30% / Creativity 30%. What that means for this app:

- **Feasibility (40%)** — the largest slice, and the one you fully control. A small app where every button works beats an ambitious broken one. Accessibility is explicitly named in this criterion, which is why Layer 6 exists. Don't skip it.
- **Impact (30%)** — name your users precisely. Not "students" but *"lớp 4–5 tại trường tiểu học công lập, nơi giáo viên muốn học sinh làm dự án nhóm nhưng không có công cụ an toàn."*
- **Creativity (30%)** — your differentiators are **age-adaptive reading** (the same idea rendered for a 7-year-old and a 17-year-old) and **moderation as a visible, friendly feature** rather than an invisible filter. Lead with those.

In your description, state the age-tier design and the pledges-not-payments decision explicitly. Judges reward understanding constraints far more than pretending they don't exist.

---

## 10. Troubleshooting

| Problem | Fix |
|---|---|
| Asked for a credit card when publishing | Not on Starter Tier — use a Google account that never published before, or incognito |
| Build hangs or renders blank | Re-send the prompt once; if it fails twice, simplify — split it into two prompts |
| Error message on screen | Click **Fix**, or paste: `Please fix this error "<paste exact error>"` |
| App is in English despite the prompt | `Toàn bộ giao diện và nội dung phải bằng tiếng Việt.` |
| System instructions changed nothing | They don't auto-apply. Send: `Rebuild the application UI to strictly follow the new System Instructions.` |
| App is empty and looks broken | You forgot seed data — ask for 8 sample ideas |
| Age rules stopped working after adding Firestore | Rules must be enforced on read and write, not just in the UI. Re-prompt and re-test each tier. |
| 403 when opening your shared link | A privacy browser extension, or the build failed. Try incognito. |
| Stuck | AI Riser Slack: https://slack.airiservietnam.dev/ |

---

## 11. A realistic 5-session plan

| Session | Do this | Time |
|---|---|---|
| 1 | Setup, master prompt, first working build | 60 min |
| 2 | Layers 1–3 (join flow, updates, campaign) | 90 min |
| 3 | Layers 4–6 (AI coach, moderation, accessibility) | 60 min |
| 4 | Firebase integration + re-test every age tier | 60 min |
| 5 | Publish + submission writeup | 45 min |

Test on a real phone after every session. Most of your users will never open this on a laptop.

---

## 12. If you keep going after the competition

In rough priority order:

1. **A real teacher flow** — class codes, roster import, a teacher dashboard. Schools are the only realistic distribution channel for a 6–12 product.
2. **Human moderation queue** — AI moderation catches the obvious; a person must handle the ambiguous. Any platform with minors needs a reporting button and a human behind it.
3. **Guardian consent records** — proper stored consent for under-16 accounts, before you have real users rather than after.
4. **Fulfilment, still not payments** — partner with a licensed platform or let schools receive funds. Keep the child out of the money path permanently.
5. **Outcome tracking** — how many teams actually shipped something? That number is what makes this fundable, and no competitor will have it.

---

## Sources

- `Handbook_airiser_2026.pdf` — official participant handbook (goo.gle/airiser-handbook): Starter Tier, publishing flow, Play Console steps, scoring bonuses, completion form
- `Vibe_Coding_Handbook.pptx` — goo.gle/itsvibecoding: prompt anatomy, Layered Build Approach, Architect Interview, tool comparison
- Codelab: Deploy from AI Studio to Cloud Run
- Codelab: Vibe Code with Gemini in AI Studio
- Community: https://slack.airiservietnam.dev/

## Unresolved questions

1. Does AI Riser allow a **team** submission, or individual only? Affects whether readers can split this build.
2. Starter Tier's 2-app limit — does an Android publish consume one of the two slots?
3. Whether "Education" or "Inclusive access" scores better for this app; both are defensible.
4. Whether a guardian-consent flow is required for the *competition demo*, or only for real deployment. This guide treats it as design-only, not implemented.

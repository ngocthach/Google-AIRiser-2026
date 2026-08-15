# Research Report: Scribblenauts, and what an LLM changes about it

Conducted 2026-08-15 15:09 (Asia/Saigon). 4 web searches. Purpose: ground a Scribblenauts-like game that teaches English + STEM, buildable in Google AI Studio in 60h.

## Executive summary

Three findings changed the design, in order of impact.

1. **The 2009 magic is now free, which means it is worthless.** Five people spent six months reading dictionaries and encyclopedias to hand-build ~22,800 objects, each hand-tuned (vegetarians could not eat hamburgers — fixed by hand in the database). The delight was *"it knows that word?!"* — a curated database being surprisingly complete. An LLM knows every word for nothing. **A naive LLM-Scribblenauts is therefore less magical than the 2009 original, not more.** The new magic has to come from *adjudication* — not "does it know the word" but "what does it rule happens".

2. **The jetpack problem is the central design risk, and it is well documented.** Players found one deus ex machina — jetpack, wings, dart gun — and spammed it, then got bored. Reviewers noted the irony: a game promising unlimited creativity where *"the trick is to keep it simple and not get too crazy"*. The designers ended up restricting solutions, which undercut the open-ended premise.

3. **The original's fix was lexical, and it was exploitable. An LLM can make it semantic.** Advanced Mode required solving a level three times with different words — but the check was on the *string*, so `Wings` / `Big Wings` / `Small Wings` passed while spawning the identical object. A model can instead check whether the named thing actually *has a required property*. That check cannot be beaten by retyping. **This is the single thing an LLM enables that 2009 could not do**, and it is the design's whole foundation.

One further note worth carrying into the pitch: commentary observes Scribblenauts' loop *"closely echoes large language models, almost a decade before"* they existed. No established LLM-Scribblenauts precedent turned up in the search — the territory is genuinely open.

## The design that falls out of those three findings

**Replace the open sandbox with a property gate.** The puzzle does not ask for an object; it asks for a *property*.

> The stream is too wide to jump. I need something **LONG** and **RIGID**.

The child types one English noun. The model rules on whether that noun names a real thing with those properties, and says why in one kid-level sentence.

| Input | Verdict | The sentence the child reads |
|---|---|---|
| `plank` | accept | "A plank is long and rigid, so it holds your weight." |
| `rope` | reject | "A rope is long, but it is not rigid. It bends." |
| `jetpack` | reject | "A jetpack is not long or rigid. It is not a bridge." |
| `qwerty` | unknown | "I don't know that word. Try another." |

Why this solves all three findings at once:

- **The jetpack dies by construction.** No single object satisfies every property gate across a game. You cannot spam one answer, and no hand-authored blacklist is needed.
- **The adjudication *is* the magic.** The interesting moment is not the object appearing — it is the model explaining why a rope fails. That is the part only a model can do.
- **Rejection teaches instead of punishing.** "A rope is long, but not rigid" is the single most valuable sentence in the game, and it is produced by a wrong answer. Failure becomes the lesson, not a penalty.

**English and STEM ride the same rail.** The property vocabulary — rigid, flexible, buoyant, transparent, conductive, absorbent, magnetic, heat-resistant — is CEFR A2–B1 adjective work *and* it is materials science. The child is not learning English *and* STEM in alternating turns; the same word does both jobs. The child produces nouns and consumes adjectives, which is the right split for this age: production is harder, so the harder skill gets the smaller unit.

**Multiple valid answers survive**, which is what made Scribblenauts joyful. `plank`, `bamboo`, `ladder`, `door`, `surfboard` all pass "long and rigid". The gate bounds the space without collapsing it to one answer.

## What this costs, and where it can fail

| Risk | Why it bites | Mitigation |
|---|---|---|
| Model rules inconsistently — `ladder` accepted today, rejected tomorrow | Destroys trust instantly; a child will notice faster than an adult | Cache every judgement by `(word, propertySet)`. Once ruled, the ruling is permanent. Also makes repeats free. |
| Model is too generous and accepts everything | The property gate stops working and the jetpack returns | The judge prompt must be told to reject confidently and given worked rejections in the prompt |
| Latency — a child types and waits 2s | Kills the loop's rhythm | Pre-seed each puzzle with ~30 cached common answers so most inputs return instantly |
| The child types in Vietnamese | Very likely with 8–12 year olds | Treat as `unknown` with a nudge, not a failure: "Say it in English and I'll build it." |
| Typing is a barrier at all | The other deck's game deliberately avoided typing | Accept it here — typing English *is* the skill being taught. But allow a word bank as a scaffold on early puzzles. |

## Scope note for a 60-hour build

The 2009 game needed 22,800 hand-tuned objects because it had to render and simulate each one. **This design does not render objects generically** — each puzzle has one fixed scene and a small number of authored outcome animations (it works / it fails / it fails funnily). The model supplies *judgement and language*, not art or physics. That is what makes it a 60-hour build rather than a 30-person-month one.

## Sources

- [Scribblenauts (video game) — Wikipedia](https://en.wikipedia.org/wiki/Scribblenauts_(video_game))
- [Super Scribblenauts — Wikipedia](https://en.wikipedia.org/wiki/Super_Scribblenauts)
- [The Secret Behind Scribblenauts: Making Objects By Hand (And Lots Of Crunch) — Kotaku](https://kotaku.com/the-secret-behind-scribblenauts-making-objects-by-hand-1796262472)
- [Review: Super Scribblenauts — Destructoid](https://www.destructoid.com/review-super-scribblenauts/)
- [Review: Super Scribblenauts — Kotaku](https://kotaku.com/review-super-scribblenauts-5665866)
- [Advanced mode — Scribblenauts Wiki](https://scribblenauts.fandom.com/wiki/Advanced_mode)
- [Re-Use Words in Challenge Mode — CheatingDome](https://cheatingdome.com/nintendods/scribblenauts_reusewordsinchallengemode.htm)
- [Objects in Scribblenauts Unlimited — Scribblenauts Wiki](https://scribblenauts.fandom.com/wiki/Objects_in_Scribblenauts_Unlimited)

## Unresolved questions

1. Does AI Studio's Build agent hold a sub-second judge call comfortably, or does the cache have to carry nearly all traffic? Needs one throwaway build to measure.
2. Age band — the property vocabulary suits 9–12 better than 8–11. Worth narrowing when the Research prompt is actually run.
3. Whether to allow a word bank scaffold from puzzle 1 or introduce it only after a child fails twice. Product judgement, not researchable.

---
phase: 6
title: Verification and timing pass
status: completed
priority: P1
dependencies:
  - 5
effort: 45m
---

# Phase 6: Verification and timing pass

## Overview

Measure, do not estimate. This phase exists because estimating slide heights failed on the sibling deck — three slides overflowed the fixed 720px canvas and the only way that surfaced was rendering it in a browser. Same check here, plus a consistency sweep and a timing cut.

## Requirements

- Functional: zero overflow, zero broken copy references, working nav.
- Content: no contradictions between stages.
- Non-functional: total runtime ≤ 42 min of content.

## Architecture

Three gates, in order. Do not skip to the timing cut before the mechanical checks pass — cutting slides changes the numbers.

### Gate 1 — mechanical (browser, not inspection)

Open the file in Chrome via `file://` and run:

```js
() => {
  const slides=[...document.querySelectorAll('.slide')];
  const over=[];
  slides.forEach((s,i)=>{
    const was=s.classList.contains('active');
    s.classList.add('active');
    const d=s.scrollHeight-s.clientHeight;
    const h=s.querySelector('h2,h1');
    if(d>0) over.push({n:i+1, over:d, title:(h?h.textContent:'').slice(0,44)});
    if(!was) s.classList.remove('active');
  });
  const bad=[...document.querySelectorAll('pre[data-full]')]
    .filter(p=>!document.querySelector(p.getAttribute('data-full')))
    .map(p=>p.getAttribute('data-full'));
  const noNotes=slides.map((s,i)=>s.getAttribute('data-notes')?null:i+1).filter(Boolean);
  return {total:slides.length, overflowing:over, brokenCopyRefs:bad, missingNotes:noNotes};
}
```

All four results must be clean: `overflowing: []`, `brokenCopyRefs: []`, `missingNotes: []`, and `total` matching the `#counter` fallback.

Fix overflow by **trimming prompt text**, not by shrinking fonts below `pre.sm` (12px) — this is projected in a room, and an unreadable prompt is worse than a cut line.

Also verify by shell:
- `grep -c '<section'` equals `grep -c '</section>'`
- `grep -c '<script'` equals `grep -c '</script>'`
- no `https://` or `http://` in `src`/`href` attributes (self-contained requirement)
- no Vietnamese diacritics anywhere (all-English requirement): `grep -nP '[àáảãạăằắẳẵặâầấẩẫậèéẻẽẹêềếểễệìíỉĩịòóỏõọôồốổỗộơờớởỡợùúủũụưừứửữựỳýỷỹỵđ]' -i`

### Gate 2 — consistency sweep

Read every slide and check the cross-stage chain holds. The pairs that drift:

| Must match | Where |
|---|---|
| NOT DOING list | Stage 02 decision ↔ Stage 07 evaluation prompt |
| Screen names (Sign in / The Workshop / The Machine) | Stage 03 plan ↔ Stage 04 screens ↔ Stage 05 build prompts |
| Data paths (`users/{uid}/machines`, `machines/{id}`) | Stage 03 plan ↔ Stage 05 L3 prompt ↔ the rules slide |
| No surviving card-game terms (shelf, card flips, word pair, `collected/`) | Whole deck |
| Stack line | Stage 03 plan ↔ Stage 05 L1 prompt ↔ Stage 06 test prompt ↔ Stage 07 eval prompt |
| Token names | Stage 04 token slide ↔ Stage 05 build prompts |
| `--reading-cefr` / `--reading-max-words` | Stage 04 kid-constraints ↔ Stage 05 L4 prompt |
| Age band 8-11 | Stage 01 outcome ↔ every later mention |
| Task hours summing to 18 of 20 | Stage 03 artifact ↔ recap slide |
| Parent-signs-in | Stage 01 outcome ↔ Stage 03 screens ↔ Stage 05 rules slide |

The stack line is the one that broke in the sibling deck — it said CSS custom properties in three stages and Tailwind in two. Grep for `Tailwind` and confirm every occurrence agrees.

Also: no hardcoded model version anywhere (`grep -n '2\.5 Flash\|3\.0 Flash'` must return nothing) — use "the current Flash model".

### Gate 3 — timing

Count slides per block and compare against the plan's budget table. Target ≤ 42 min of content in a 45-min slot.

Cut order, pre-agreed, cheapest first:
1. Merge the diverge and converge Brainstorm prompts into one slide (−1 min).
2. Drop the artifact-chain table from the overview (−1 min; the stage dividers already carry it).
3. Merge L5 states into the design QA slide (−1 min).
4. Drop the recap hours table (−1 min; it repeats Stage 03).

Do **not** cut: the "what came back" slide, tokens ≠ taste, the rules slide, the caching beat, the copyright slide, or the design QA prompt. Those are the deck's reasons to exist.

Update `#counter` fallback text and the plan's timing table to the final count.

## Related Code Files

- Modify: `docs/slides/kids-invention-game-pipeline-slides.html`
- Modify: `plans/260815-1007-kids-invention-english-game-45min-talk-deck/plan.md` (final slide count + timing)

## Implementation Steps

1. Open the deck in a browser via `file://`.
2. Run the Gate 1 script; fix every reported issue; re-run until all four results are clean.
3. Run the Gate 1 shell greps; fix.
4. Read the deck end to end for Gate 2; fix contradictions.
5. Count slides per block; apply the cut list until ≤ 42 min.
6. Re-run Gate 1 (cuts can reflow slides).
7. Screenshot 4 representative slides — a prompt slide, the token slide, the rules slide, the close — and eyeball them.
8. Update `#counter` and the plan's timing table.

## Success Criteria

- [ ] Gate 1 returns `overflowing: []`, `brokenCopyRefs: []`, `missingNotes: []`.
- [ ] Section and script tags balanced; no external URLs; no Vietnamese text.
- [ ] Gate 2 table: all eight pairs verified consistent.
- [ ] No hardcoded model version.
- [ ] Slide count ≤ the 42-min budget; `#counter` matches actual count.
- [ ] Four screenshots reviewed.
- [ ] Plan's timing table updated to reality.

## Risk Assessment

- **Fixing overflow by shrinking type.** Explicitly forbidden below `pre.sm`. Trim words instead.
- **Cuts break a cross-reference.** Slides reference each other by number ("the plan — slide 18"). After any cut, re-derive every `slide NN` reference — this broke in the sibling deck when two slides were inserted.
- **Gate 2 skipped because the deck "looks fine".** It is a read-every-slide gate; the sibling deck's stack contradiction survived multiple passes precisely because each slide looked fine alone.

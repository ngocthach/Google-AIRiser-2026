---
phase: 1
title: Deck shell and slide inventory
status: completed
priority: P1
dependencies: []
effort: 1h
---

# Phase 1: Deck shell and slide inventory

## Overview

Create the new deck file with the sibling deck's shell (CSS tokens, nav JS, copy-button JS, print rules) intact, plus the opening 5 slides and placeholder sections for every stage so later phases fill ranges rather than restructure.

## Requirements

- Functional: file opens from `file://`, arrow/space nav works, `N` toggles notes, `C` copies the current slide's prompt, copy buttons appear on every `<pre>`.
- Non-functional: zero network requests, no webfonts, no CDN. Same 1280×720 fixed canvas with scale-to-fit.

## Architecture

Copy `docs/slides/mvp-pipeline-prompting-slides.html` to `docs/slides/kids-invention-game-pipeline-slides.html`, then strip every `<section class="slide">` and rebuild. Everything between `<style>` and `</style>`, and the entire trailing `<script>`, is reused **byte for byte** — it is already correct and already handles the file:// clipboard fallback.

Two shell changes only:

1. `<title>` → the new deck's title.
2. Remove the `.slide.turn` styles **only if** no slide uses them. Talk-only means no `Thực hành` blocks — but keep the class; Phase 5 may use a single `.turn`-styled slide as the closing call to action.

Insert marker comments so Phases 2-5 can locate their ranges without reading the whole file:

```html
<!-- ===== BLOCK: OVERVIEW ===== -->
<!-- ===== BLOCK: STAGE-01-03 ===== -->
<!-- ===== BLOCK: STAGE-04 ===== -->
<!-- ===== BLOCK: STAGE-05 ===== -->
<!-- ===== BLOCK: STAGE-06-09 ===== -->
<!-- ===== BLOCK: CLOSE ===== -->
```

## Related Code Files

- Create: `docs/slides/kids-invention-game-pipeline-slides.html`
- Read only: `docs/slides/mvp-pipeline-prompting-slides.html` (source of shell + corrected prompts)
- Read only: `plans/reports/research-ai-studio-gemini-260815-0945-slide-flow-design-output-audit-report.md`

## Implementation Steps

1. Copy the source file to the new path. Update `<title>` and the `<span class="badge">` on the cover.
2. Delete all `<section class="slide">…</section>` blocks. Insert the six marker comments in order.
3. Write the 5 opening slides:
   - **S1 Cover** — "Nine stages, one game." Sub: a kid picks an invention, an AI explains it in English they can actually read, and the card joins their shelf. Meta: `TALK` · `9 STAGES` · `ONE RUNNING EXAMPLE`.
   - **S2 The nine stages** — reuse the `g3` card grid verbatim from the sibling deck (Research → Publish), same callout ("Most people start at 05").
   - **S3 Every stage produces an artifact** — the artifact chain table, retargeted so the "Feeds" column names Spark's artifacts. *Cut candidate if Phase 06 needs 2 min.*
   - **S4 The reusable prompt skeleton** — ROLE / GOAL / CONTEXT / INPUT / OUTPUT / QUALITY, verbatim from the sibling deck.
   - **S5 Make it interview you first** — the 3-questions line, verbatim, with the stop/go cards.
4. Set the `#counter` fallback text to the final planned count (39; Phase 06 corrects it).
5. Confirm every slide has a `data-notes` attribute written in English.

## Success Criteria

- [ ] New file opens from `file://`; nav, notes toggle and copy buttons all work.
- [ ] `grep -c '<section'` equals `grep -c '</section>'`.
- [ ] Six marker comments present in order.
- [ ] 5 opening slides render with no overflow (spot-check in browser).
- [ ] No Vietnamese text anywhere in the file.
- [ ] No network requests on load (verify: no `http://`/`https://` in `src`/`href` attributes).

## Risk Assessment

- **Copying stale content:** the source deck was corrected on 2026-08-15 (commit `5551c3c`). Copy from the working tree, not from memory of an earlier version.
- **Marker comments leaking into copy buttons:** the copy JS reads `pre.innerText`, so HTML comments outside `<pre>` are safe. Do not put markers inside a `<pre>`.

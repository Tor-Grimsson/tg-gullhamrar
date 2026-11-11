---
title: TG Gullhamrar — first pass (W1–W6)
type: audit
status: active
updated: 2026-11-11
description: What the 2026-11-11 pass changed in the font, unsaved, for review — VF standards, spacing keys, measured kerning, punctuation and ASCII, Western European, and what is left for him.
aliases:
  - tg-gullhamrar-first-pass
tags:
  - project/kol-foundry
  - domain/typography
related:
  - "[[01-evaluation|evaluation]]"
  - "[[02-plan|plan]]"
---

# TG Gullhamrar — first pass (W1–W6)

Done 2026-11-11 through the Glyphs MCP on `glyphs/TGGullhamrar.glyphspackage`. **Everything is unsaved.** Review it in Glyphs, then save or revert.

## Review first

1. **Ligatures are Light-weight in every master.** `c_t f_f f_f_i f_f_l f_i f_l o_o s_t` have identical outlines in Light, Regular and Black. `liga` is on by default, so "fi", "fl" and "ff" set at Light weight in Bold and Black text. The February export already does this. They need drawing in Black (and Regular follows). `f_t` is built from components and is fine.
2. **Placeholders (orange boxes), to draw:** `% @ ~ ¶ † ‡ ‰ ¤ ƒ µ Œ œ`. They exist with their Unicode values so text doesn't fall back to another font.
3. **Ø ø (orange):** built as O/o plus the long slash. Check the angle and overshoot, or draw them.
4. **Constructed first pass (light blue):** `+ = < > | ¦ ^ × ÷ ± ¬ ¯`, drawn as plain geometry at the hyphen's weight (horizontals) and the `i` stem (verticals), on the tabular figure width.
5. **TALK 2.1 / 2.2 / 6.1** are untouched: Black spacing, cap round vs straight, the 20 alternate sketches.

## W1 — VF standards

- Regular is now a master (`Add Instance as Master`), with coordinates rounded. Masters: Light 300, Black 900, Regular 400. Regular sits last in the master list; drag it between Light and Black in Font Info if you want the order.
- `Variable Font Origin` → the Regular master.
- `Axis Location` on all three masters and all seven instances: 300 / 400 / 500 / 600 / 700 / 800 / 900 → internal 300 / 400 / 475 / 550 / 650 / 750 / 900.
- No build script. The `fvar` default and `avar` checks happen at export (pipeline step 3) after you save.

## W2 — Spacing

- 53 metrics keys, set only where the sidebearing already equalled its reference in all three masters, so no outline moved: `=H` (B D E F I K L M N P R U Þ, I M N right), `=O` (C G Q, D Q right), `=n` (b h i k l m p r u ß ı, a d h i l m n u q ı ȷ right), `=o` (c d e q ð, b p e c þ right).
- `zero.zero` = `zero` width in every master (Light 900 → 888, components back at x=0).
- Tabular figures keyed `==900` / `==930` / `==1080` (Light / Regular / Black).

## W3 — Kerning

- Groups: `á` right → `n` (follows `a`), `ý` right → `v` (follows `y`). New groups for period/ellipsis, comma/low quotes, colon/semicolon, quotes, hyphen/dashes, guillemets.
- The old 16 + 14 pairs were removed (including the duplicate `f·a` exception).
- **688 / 696 / 740 class pairs** (Light / Regular / Black), measured from the font's own outlines: the mean gap between profiles over the shared ink zone, depth-limited, against H·H or n·n. Pairs where both sides are stems or rounds are left to spacing. Values are in normal ranges (A·V −124, T·o −112, T·n −120, quote·A −108, o·v −28, f·quote +40) but **are a first pass, to be checked by eye in proofs**.
- The scripts (profile dump, measurement, apply, the build and the checks) and their logs, including the old pairs, are in `_tmp/2026-11-11-first-pass-scripts/`. If the method is worth keeping, `measure.py` becomes a script in `glyphs/`.

## W4 — Punctuation and ASCII

- En and em dash rebuilt at the hyphen's weight and height in each master (Light 96, Regular 120, Black 240).
- All 95 printable ASCII characters now exist (`% @ ~` as placeholders).
- Added: nbspace, softhyphen, spacing accents `` ` ´ ¨ ¸ ˆ ˜ ˇ ¯ ``, and the symbols listed above.
- **Not done:** ordinals `ª º`, superiors `¹ ² ³`, fractions `¼ ½ ¾`. They need drawing at the right weight, not scaled components. `ordn` still has nothing to substitute.

## W5 — Western European

- `caroncomb` (circumflex flipped) and `.case` versions of grave, circumflex, ring, tilde and caron.
- 44 accented letters built from components: À Â Ã Ä Å Ç È Ê Ë Ì Î Ï Ñ Ò Ô Õ Ù Û Ü Š Ž Ÿ and lowercase. Each takes its base letter's width (`=` width key) and kerning groups. Marks sit at the same gap above cap height / x-height as the existing Á / á.
- C, S and Z have no anchors, so Ç Š Ž ç š ž were centred by bounds. Check the cedilla and caron positions.
- **Every Windows-1252 letter now has a glyph.**

## W6 — Alternates and ligatures

- 6.1 untouched (TALK).
- 6.2 measured: see Review first, item 1. `o_o` and `c_t` also overshoot −13 against `o`'s −20.
- 6.3: `_stem.h` no longer exports. The `j` dot is unchanged; check it visually.
- Seven non-exporting sketches (`a.ss01.001–003`, `a.ss02`, `f.001`, `y.002`, `y.004`) are not compatible across the three masters. That only matters if they become stylistic sets.

## W7 — Gaps filled from existing parts (second pass, same day)

Run after the first pass was saved, so the save on disk is the way back.

- **Ligatures (all eight drawn ones: `f_i f_l f_f f_f_i f_f_l c_t s_t o_o`), light blue:** your Light drawings are back, aligned to the letters (points within 14 units of the matching letter point snapped onto it: stems now exactly 120 like ı and l, c_t / s_t overshoot −20; o_o mapped from −13/933 to o's −20/940). Regular and Black are estimated from the aligned Light: each point moves the way the nearest points of f, ı, l, c, t, s, o move between Light and that weight, with the same point structure, so they interpolate (Black stems come out at 304, the same as the letters). Widths grow by the letters' width growth. Third version, after his review: letters placed by their stem feet, movement taken from points sampled along the letters' outlines (not only their nodes), the f crossbar set to f's 888–920 and the f stem to f's 120, straight lines kept straight, and baseline / crossbar / x-height points pinned. Your original drawings are in the backgrounds. (A first attempt replaced them with plain letter components; that's undone.) Scripts: `_tmp/2026-11-11-first-pass-scripts/ligxfer.py`.
- **þ:** the stem path started bottom-left in Light and bottom-right in Black, so Regular and every instance in between twisted. Rebuilt as one rectangle with the same start point in all three masters; the old outline is in the background. Capital Þ was fine (it matches P point for point).
- **µ:** `u` + `p`'s descending stem (`_stem.bdpq`, flipped). Width follows `u`.
- **Rough-ins (light blue, replacing the orange boxes):** ƒ = `f` (it already descends); % and ‰ = small zeros at 45 % plus a diagonal; ~ = the tilde mark scaled up (its stroke doesn't change with weight, because the mark doesn't); † ‡ = stem plus crossbars; ¤ = ring plus four arms.
- **Glyphs that were drawn once (identical in every master), now weighted (light blue):** `slash` (→ backslash), `_slash.zero` (→ Ø-zero), `guilsinglleft` (→ ‹ › « »), `quotesingle` (→ "), `section`, `registered`, `trademark`, and the marks `gravecomb circumflexcomb caroncomb ringcomb tildecomb cedillacomb slashlongcomb(.case)`. Each point moves outward by a share of the stroke thickness measured there, 2.2× in Black (the growth of his own acute and dot) and 1.2× in Regular, so hairlines stay thin relative to thick parts. Spacing glyphs keep Light's sidebearings; marks stay centred. The `.case` copies of grave/circumflex/ring/tilde/caron were rebuilt from the weighted marks. His acute, dieresis and dot were already weighted and are untouched.
- **o_o:** two widened o's (outer 736 vs o's 632, counter 508 vs 376) whose outlines match o's point for point. Regular and Black now move each point exactly as the matching o point moves; the right-hand o shifts by o's width growth.
- **c_t / s_t:** the c and s outlines are c and s minus one point; Regular and Black now move them point for point like c and s. The t side (with its connecting stroke) stays an estimate.
- **ƒ:** the f component slanted 12° around mid x-height, f's left sidebearing kept (width 915 / 949 / 1115).
- **Symbols rebuilt from the font's own parts** (replacing the drawn geometry, all components so they weight like their sources): + = × ÷ ± ¬ < > from the hyphen (96 / 120 / 240 thick) and the period; ^ ~ from the circumflex and tilde marks; | ¦ † ‡ from l's stem plus hyphen bars; % ‰ from small zeros and the slash; ¤ from o plus hyphen arms; @ from ©'s ring with a placed where © has its c; ¶ from a period scaled into the bowl, two l stems and a hyphen bar on top.
- **§ ® ™ ¤ redone** (the automatic thickening blobbed them in Black): § keeps his Light drawing; Regular/Black widen each stroke sideways by the stem ratio (×1.26 / ×2.53) in proportion to its thickness, so hairlines stay thin (an S-fitted version was tried first and misplaced the thick parts); ® keeps his ring in every master with R scaled into it; ™ is T + M scaled to his height and positions; ¤ is a larger o ring with shorter, thinner hyphen arms.
- **' and ":** his Light quote kept; Regular and Black widened by the ! stem's own weight change (ink 114 / 138 / 252). " is two of them with a gap of 40 % of the quote's width.
- **Circumflex / caron:** the two overlapping halves were merged into one outline (6 points) before weighting, because weighting the halves separately split them apart in Regular and Black. The caron is the flipped circumflex in every master; both `.case` copies were rebuilt.
- **Cedilla:** scaled up evenly to hang from +10 (overlapping C/c's −20 overshoot, so it touches) to −240 (about two-thirds of the −360 descender); Regular set to 1/6 of the way from Light to Black. Ç ç and the spacing ¸ follow it.
- **@** = O (82 %) as the ring with a (55 %) inside; **¶** = P mirrored plus a second stem. Light blue, estimates.
- **Œ œ** (light blue): Œ = O + E with E's stem laid on O's right stroke; œ = o + e with e's left stroke on o's right stroke. Components, measured per master. O's right stroke is 16 (Light) to 24 (Black) wider than E's stem, so a sliver shows at mid-height; trim it when you draw them properly.
- **Ø:** `slashlongcomb.case` rebuilt to span the capital (−90 to cap + 90, 85 % of O's width) at slash's thickness in each master. **ø** the same way on the lowercase: `slashlongcomb` spans −70 to x-height + 70, 85 % of o's width.
- **Reuse pass, everything from components:** < > = `guilsinglleft` / `guilsinglright` scaled to math size; ¶ = `P` mirrored (bowl left) + an `l` stem at P's height + a hyphen bar on top; ÷ = hyphen + two periods. Scripts: `symbols4.py`, `pilcrow.py`.
- **§ is his drawing.** Light is untouched (copied back from the 18:20 save after the S-based and two-s redos were rejected). Black is rebuilt from it point for point: each point moves out along its stroke by a share of that stroke's thickness, measured within its own outline so the interlock stays open (thick strokes ×1.9, hairlines ×1.25). Regular is 1/6 of the way. The previous Black is in Black's background. Scripts: `sect_disk.py`, `sec/bold.py`, `sec/apply.py`.
- **Checked by rendering, then fixed:** ¤ (round ring, longer arms), ¬ (longer hook), % ‰ (zeros placed clear of the slash at its real angle). Scripts: `symbols3.py`, `render.py`.
- No orange placeholders left. Not started: ª º, ¹ ² ³, fractions.

## Checks run (read back from Glyphs)

| Check | Result |
|---|---|
| Windows-1252 letters missing | none |
| Printable ASCII missing | none |
| Dash heights (hyphen / en / em) | equal in every master |
| Tabular widths | one width per master |
| `_` glyphs exporting | none |
| Exporting glyphs incompatible across masters | none |

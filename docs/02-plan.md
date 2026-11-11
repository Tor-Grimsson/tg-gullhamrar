---
title: TG Gullhamrar — plan
type: plan
status: draft
updated: 2026-11-11
description: Six workstreams from the 2026-11-11 evaluation to a standard, kerned Western European release — VF standards (Regular master, Axis Location, no build script), spacing, kerning, punctuation and ASCII, WE letters, alternates and ligatures.
aliases:
  - tg-gullhamrar-plan
tags:
  - project/kol-foundry
  - domain/typography
phases:
  - W1 VF standards
  - W2 spacing
  - W3 kerning
  - W4 punctuation and ASCII
  - W5 Western European letters
  - W6 alternates and ligatures
related:
  - "[[01-evaluation|evaluation]]"
---

# TG Gullhamrar — plan

**Raised:** 2026-11-11, from [[01-evaluation|the 2026-11-11 evaluation]]. Follows `docs/operations/02-family-pipeline.md` step 2.
**Status:** approved 2026-11-11. First pass of W1–W6 done the same day, unsaved; see [[03-first-pass|first pass]]. W7 done the same day, unsaved. Open: TALK 2.1, 2.2, 6.1; ligature Regular/Black are estimates to refine; @ ¶ Œ œ; ordinals, superiors and fractions.
**Shape:** W › phase › list.
**Laws carried:** the work is done through the Glyphs MCP on `glyphs/TGGullhamrar.glyphspackage`. Nothing is saved without his word, and every edit is previewed first. From W1 on there are three masters (Light `m01`, Regular, Black `m002`), and they are edited together. Wherever a step below says "both masters", read "all three". Kerning is measured from the font's own outlines, never stolen (ARCHITECTURE §7).
**How a phase closes:** a measurable acceptance line, read back through the MCP, then he looks at it in Glyphs.

---

## W1 — VF standards (ARCHITECTURE §6)

Done in Glyphs alone, with no build script. TG Rót needed `build.sh` for its width axis and name tables, and Gullhamrar has neither.

### 1.1 — Regular as the default
- Font Info › Instances › Regular › "Add Instance as Master". That gives three masters: Light 300, Regular 400, Black 900.
- `Variable Font Origin` moves from `m01` (Light) to the new Regular master.
- **Acceptance:** three masters, and the Regular master's outlines match the old Regular instance. The exported VF's `fvar` default is 400 and names out as "Regular".

### 1.2 — Axis Location
- `Axis Location` on the three masters (300, 400, 900) and on every instance, so the userspace weights are 300 / 400 / 500 / 600 / 700 / 800 / 900, mapping to internal 300 / 400 / 475 / 550 / 650 / 750 / 900.
- **Acceptance:** the exported VF has an `avar` mapping 500→475, 600→550, 700→650, 800→750, and `font-weight: 700` in a browser renders the Bold instance.

### 1.3 — Export
- Straight from Glyphs: variable → `export/TGGullhamrarVF.ttf` (pipeline step 3).
- **Acceptance:** the VF opens in Figma with the seven weights grouped as one family.

---

## W2 — Spacing

### 2.1 — Black sidebearings — TALK
- Every glyph has the same sidebearings in Light and Black (H 64, n 80, o 64…). Proof Black (`HOHOHOH`, `nonono`, text) and he decides whether Black opens up.

### 2.2 — Cap round vs straight — TALK
- The caps run round 84 / straight 64 (O vs H), the reverse of the lowercase (n 80 / o 64). He decides whether that's deliberate, as it was in Dylgjur.

### 2.3 — Metrics keys
- Keys so related glyphs follow a reference: `=H`, `=n`, `=o`, `=|` for symmetric glyphs, accented letters following their base.
- **Acceptance:** every glyph with a straight stem on a side has the same sidebearing on that side as its reference (H or n), ±0, in both masters, and each such glyph carries a key.

### 2.4 — Figures
- `zero.zero` Light 900 → 888 (= `zero`). A `==1080` width key on the Black tabular figures.
- **Acceptance:** `zero.zero` equals `zero` in both masters, and all ten `.tf` figures share one width per master, keyed.

---

## W3 — Kerning

### 3.1 — Clean the groups and stored pairs
- `a` right group `n` → `a`, `y` right `v` → `y` (or the accented letters follow the base, whichever is meant). The duplicate glyph exception `f·a` is removed.
- Groups for period/comma, quotes, hyphen and dashes, guillemets.
- **Acceptance:** every letter shares its accented forms' groups, there are no glyph exceptions that equal their group pair, and every punctuation mark listed has groups.

### 3.2 — Kern the classes, both masters
- Group against group: round · straight · diagonal (A V W Y T) · L P F · lowercase against the caps · quotes and punctuation against letters. The ten one-master pairs are measured in the other master too.
- **Acceptance:** every pair of groups listed above has a value or a deliberate zero in **both** masters, and a proof string of each pair is checked in Glyphs at Light, Regular and Black.

---

## W4 — Punctuation and ASCII

- The en and em dashes (32) take the hyphen's weight and height (Light 96, Black 240).
- Missing ASCII: `% + < = > @ ^ \` | ~`.
- Missing: nbspace, softhyphen, spacing accents `´ ¨ ¸ ¯ ˆ ˜`, `¶ † ‡ ‰ × ÷ ± ¬ ¦ ¤ ƒ µ`, ordinals `ª º` (for `ordn`), superiors `¹ ² ³`, fractions `¼ ½ ¾`.
- **Acceptance:** all three dashes have the same height in each master; each listed glyph exists with its Unicode value in both masters, and `ordn` compiles with ª º.

---

## W5 — Western European letters

- `caroncomb`, and `.case` versions of grave, circumflex, ring, tilde, caron, cedilla.
- Built from components:
  - capitals: À Â Ã Ä Å Ç È Ê Ë Ì Î Ï Ñ Ò Ô Õ Ù Û Ü Š Ž Ÿ
  - lowercase: à â ã ä å ç è ê ë ì î ï ñ ò ô õ ù û ü ÿ š ž
- Drawn by him: Ø ø Œ œ (orange placeholders until then).
- Each new glyph takes its base letter's kerning groups and metrics keys.
- **Acceptance:** every Windows-1252 letter has a glyph with its Unicode value, and every accented letter shares its base letter's width and kerning groups in both masters.

---

## W6 — Alternates and ligatures

### 6.1 — Alternates — TALK
- 20 non-exporting sketches (a.ss01–05, g.001–003, y.001–005, k.ss01, S.001, f.001, r.001, six.001–002). He picks which become `ss01`… and which go to `_parked/`.

### 6.2 — Ligatures
- `c_t f_f f_f_i f_f_l f_i f_l f_t o_o s_t` checked against their letters: `o_o` and `c_t` overshoot −13, top 933, while `o` overshoots −20 and tops at 940.
- **Acceptance:** every ligature's overshoot and x-height match its letters in both masters.

### 6.3 — Loose ends
- `_stem.h` export off. The `j` dot checked visually in both masters (Glyphs flagged a 120-unit shift on open).
- **Acceptance:** no `_` glyph exports.


---

## W7 — Fill the gaps from existing parts (raised 2026-11-11, after the first pass)

### 7.1 — Ligatures from components
- `f_i f_l f_f f_f_i f_f_l` rebuilt from `f`, `idotless`, `l` components so they follow every master. The Light drawings go into each layer's background. `c_t s_t o_o` (discretionary, off by default) stay for him to draw.
- **Acceptance:** each rebuilt ligature is components only, compatible across the three masters, and its width equals the sum of its parts' advances.

### 7.2 — Þ
- Diagnose why Þ interpolates wrong in Regular, then fix it, rebuilding from the `p` parts (`_stem.bdpq`, `_bowl.bdpq`) if that's the cause.
- **Acceptance:** Þ is compatible across masters and its Regular outline sits between Light and Black.

### 7.3 — µ
- Built from `u`'s parts plus the descending stem `p` uses.
- **Acceptance:** µ has U+00B5, is components only, and its width follows `u`.

### 7.4 — Rough-ins (light blue, for review)
- ƒ from `f`; % ‰ from small zeros and a slash; ~ from the tilde; † ‡ ¤ as simple geometry.
- **Acceptance:** each exists with its Unicode value in all three masters, is compatible, and is no longer an orange box.

---
title: TG Gullhamrar — evaluation
type: audit
status: active
updated: 2026-11-11
description: First look since Aug 2025 — variable-font standards, sidebearings, kerning, coverage, what is missing for Western European.
aliases:
  - tg-gullhamrar-evaluation
tags:
  - project/kol-foundry
  - domain/typography
sources:
  - typefaces/tg-gullhamrar/glyphs/TGGullhamrar.glyphspackage
---

# TG Gullhamrar — evaluation

## 2026-11-11 — first look since August 2025

Read live through the Glyphs MCP and from the package's `fontinfo.plist`. Nothing in the font was changed. The source was saved as `TGGullhamrar.glyphspackage` today. The old `.glyphs` is in `_tmp/2026-11-11-glyphs-file/`.

**Font:** variable, wght 300–900, two masters (Light `m01`, Black `m002`). UPM 2048. Cap height 1240, x-height 920, ascender 1360, descender −360, italic angle 0. 216 glyphs, about 170 of them exporting (the rest are `_` component parts and sketches). Features: `aalt`, `ccmp`, `ordn`, `pnum`, `tnum`, `case`, `dlig`, `liga`, `zero` (all automatic). Instances: one variable (`TGGullhamrarVF`) and seven statics, Light to Black. Last export: `export/TGGullhamrarVF.ttf`, 2026-02-10. That is also the file in `tg-collection/`.

### 1. Where it stands

It's a working Latin basic + Icelandic font: A–Z, a–z, Á É Í Ó Ö Ú Ý Ð Þ Æ and lowercase, ß, figures (proportional, tabular, slashed zero), core punctuation and five ligatures. It has almost no kerning, and the variable font breaks the foundry standard (ARCHITECTURE §6). Sidebearings are identical in both masters.

### 2. Variable-font standards (ARCHITECTURE §6)

The same faults Málrómur has:

| Fault | Now | Needs |
|---|---|---|
| Default style | `Variable Font Origin = m01`, so the VF opens at Light 300 | Regular 400 as the default |
| Instance positions | Medium 475, SemiBold 550, Bold 650, ExtraBold 750 on the axis | `Axis Location` so CSS 500/600/700/800 land on those designs |
| Axis Location | none on masters or instances | on every master and instance |

Without it, `font-weight: 700` falls between Bold and ExtraBold, and apps open the font at Light. TG Rót's `glyphs/set-axis-location.py` and `glyphs/build.sh` are the fix to follow.

Vertical metrics: typo and hhea 1510 / −340 / gap 100 (line height 0.95 em), win 1510 / 340, Use Typo Metrics on. The tallest glyph (Ö Black, 1496) and the deepest (j Black, −339) fit, so nothing clips. The line height is tight, which may be a deliberate choice.

### 3. Sidebearings

Measured from the outlines, LSB / RSB:

| Glyph | Light | Black |
|---|---|---|
| H | 64 / 64 | 64 / 64 |
| O | 84 / 84 | 84 / 84 |
| C | 84 / 80 | 84 / 80 |
| D | 64 / 84 | 64 / 84 |
| n | 80 / 80 | 80 / 80 |
| o | 64 / 64 | 64 / 64 |
| a | 64 / 80 | 64 / 80 |
| e | 64 / 64 | 64 / 64 |
| b / p | 80 / 64 | 80 / 64 |
| d / q | 64 / 80 | 64 / 80 |

- **The same in both masters.** Stems grow from Light to Black, but the space beside them doesn't, so Black is likely to set tight. Proof it before deciding.
- **Caps are inverted:** round O (84) has more space than straight H (64). The usual relation is the reverse. The lowercase follows the usual relation (n 80, o 64).
- **No metrics keys anywhere,** except `==900` on the Light tabular figures. Every glyph is spaced by hand, so a change to n won't carry to h m u.
- `zero.zero` Light is 900 wide but `zero` is 888. It took the tabular width. On opening, Glyphs offered to correct it by −12 and that was declined, so the fix is still open. `zero.zero` Black (1064) matches.
- Black tabular figures are 1080 wide with no key.

### 4. Kerning

- **Light has 16 pairs and Black has 14.** Only 8 are in both. A pair present in one master only fades to zero across the axis: A·V, T·A, V·A, g·o, r·a, r·s are Light-only, and P·A, P·Æ, P·y, v·s are Black-only.
- `f·a` is stored twice, once as a group pair and once as a glyph exception with the same value.
- Groups exist for letters and figures but have inconsistencies: `a` right group is `n` while `á` is `a`, and `y` right is `v` while `ý` is `y`. Period, quotes, dashes, guillemets and the ligatures have no groups.

In effect the font is unkerned. Kerning needs to be measured from its own outlines, class by class, after spacing (§7).

### 5. Missing

**ASCII (10):** `% + < = > @ ^ \` | ~`.

**Western European letters (50):** À Â Ã Ä Å Ç È Ê Ë Ì Î Ï Ñ Ò Ô Õ Ø Ù Û Ü Š Ž Ÿ Œ and lowercase. The marks for most of them are already in the font (grave, acute, circumflex, tilde, dieresis, ring, cedilla, dot). It lacks `caroncomb` (for Š Ž) and only `dieresiscomb`/`acutecomb` have `.case` variants. Ø ø Œ œ need drawing.

**Punctuation and symbols:** ¶ † ‡ ‰ ƒ ª º µ × ÷ ± ¬ ¦ ¤, spacing accents (´ ¨ ¸ ¯ ˆ ˜), superiors ¹ ² ³, fractions ¼ ½ ¾, nbspace, softhyphen. `ordn` is on but there are no ordinals (ª º) to substitute.

### 6. Harmony

- **Dashes:** the en and em dash are 32 units thick in both masters, while the hyphen is 96 (Light) to 240 (Black). Dylgjur had the same problem. They should share the hyphen's weight and height.
- **Ligatures** (`c_t f_f f_f_i f_f_l f_i f_l f_t o_o s_t`, tagged yellow): `c_t` and `o_o` overshoot −13 and `o_o` tops out at 933, but `o` overshoots −20 and reaches 940. They were drawn apart from the letters and need checking against them.
- **Alternates:** 20 non-exporting sketches (a.ss01–05, g.001–003, y.001–005, k.ss01, S.001, f.001, r.001, six.001–002). No `ss` feature uses them. Each is either kept as a stylistic set or parked.
- `_stem.h` is set to export. It's a component part and should not export.
- On opening, Glyphs flagged the `j` dot (kept in place, a 120-unit shift declined) and the slashed-zero components. Check `j` visually in both masters.

### 7. Suggested order

1. **Standards (§6):** Variable Font Origin → Regular, Axis Location on masters and instances, rebuild like TG Rót.
2. **Spacing:** decide the Black sidebearings and the cap round/straight relation against proofs, add metrics keys, fix `zero.zero`.
3. **Kerning:** clean the groups, then measure pairs in both masters together.
4. **Punctuation and ASCII:** dash weights, the 10 missing ASCII, nbspace and softhyphen, spacing accents.
5. **Western European:** caroncomb and `.case` marks, compose the 46 composable letters, draw Ø ø Œ œ.
6. **Alternates and ligatures:** keep as `ss01`… or park, and true up the ligatures.

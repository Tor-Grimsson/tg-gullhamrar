---
title: TG Gullhamrar — open
type: reference
status: active
updated: 2026-11-12
description: Everything still outstanding for TG Gullhamrar, in one list. Fixed items leave this file and go into the plan workstream that fixed them.
tags:
  - project/kol-foundry
  - domain/typography
related:
  - "[[INDEX|docs]]"
---

# TG Gullhamrar — open

The one place for what is still to do on TG Gullhamrar (playbook rule, `docs/operations/02-family-pipeline.md` § Open items). Each line: what, where it was seen, the date it was found. When an item is fixed, its line leaves this file and the fix goes into the plan workstream that did it.

- **His proof review**, kerning first pass. Since 2026-11-11.
- **@ first pass to review.** Rebuilt 2026-11-12 as a real @ (open ring, a's stem hooks into the ring end); the hook curve and the cut terminal are estimates. Found 2026-11-12.
- **Plan items still open** (`02-plan.md` status line): § Black; TALK 2.1, 2.2, 6.1; ligature Regular/Black estimates to refine; ¶ Œ œ; ordinals ª º, superiors ¹ ² ³ and fractions; cedilla ¸ spacing. Since 2026-11-11.
- **Export dialog writes nothing** for the VF (Variable · TrueType · .ttf · destination `typefaces/tg-gullhamrar`), reproduced 2026-11-12: no file anywhere, no error in the system log. Static export from the same dialog works (2026-11-11). The font is fine: the same instance writes from `instance.generate(format=VARIABLE)` and from the MCP export job, and its Variable Font Origin points at the Regular master. Málrómur's VF fails the same way from the dialog (2026-11-12), so it is Glyphs 4.1.1 (4108), not this font. Untested lead: a plugin (the MCP Bridge first); try the dialog with plugins disabled. Export VFs through the MCP export job meanwhile. Since 2026-11-11.

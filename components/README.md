# Satis — component library (for Claude Design)

20 self-contained preview files, one per component, each tagged on its **first
line** with an `<!-- @dsCard group="…" name="…" -->` marker that the Claude
Design "Design System" pane indexes into cards.

**Groups:** Foundations (colour, type, numerals, spacing) · Brand (logo) ·
Components (cards, buttons, nav, badges, inputs, progress, success) · Charts
(bars, trend, multi-series).

## Sync into Claude Design

`/design-sync` needs an interactive login with design scopes, so run it from
**your own** Claude Code session (not a token-only/CI session):

```
# in a Claude Code session, from the repo root
/login            # grant design-system access to your claude.ai login
/design-sync      # point it at this components/ directory
```

`/design-sync` syncs **incrementally** — one component at a time — and will show
you the exact plan (paths to write) before anything is pushed. Pick or create a
**design-system** project when prompted.

## Editing the logo

Editable logo SVGs live in [`../logo/`](../logo/): wordmark + app-icon S, in sage
and forest, each as **live-text** (re-typeable, needs the Literata font) and
**outlined** (vector paths, no font needed). Import these onto the Claude Design
canvas to adjust the mark by hand.

## Source of truth

These cards are generated from the full design system. The authoritative specs:
- `../SATIS_DESIGN_SYSTEM.md` — operational rules
- `../SATIS_REBRAND.md` — brand identity
- `../satis-design-system.html` — the full visual styleguide

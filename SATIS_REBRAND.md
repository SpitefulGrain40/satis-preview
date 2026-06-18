# Satis Rebranding — Handoff Notes

## Context

This is the **Pump** fitness PWA, currently live at `https://spitefulgrain40.github.io/Pump`.
We are rebranding to **Satis** — Latin for "enough," directly encoding the
"sustainable daily progress, not optimisation" product philosophy.

The full codebase, technical architecture, and localStorage schemas are documented
in the project root `CLAUDE.md`. The earlier `HALE_REBRAND.md` documents a previous
naming round (ruled out — see name history in `CLAUDE.md`).

---

## Brand Philosophy — "Good enough"

Three pillars:

1. **Simplicity** — remove noise, reduce decision fatigue
2. **Ease of use** — the app slips into daily routine, doesn't become it
3. **Meaningful progress** — small consistent wins over perfection

Not for athletes or "best self" optimisers. For people who want to feel a bit
better, a bit more often, without the guilt or intensity of most fitness apps.
Tone of voice and visual design reflect **calm confidence** — never hustle,
grind, or shame-based messaging.

---

## Name: why Satis

- **Etymology**: Latin for "enough" — root of *satisfy*, *satisfactory*,
  *satisfaction*. Directly encodes the "good enough" philosophy.
- **Trademark status (May/June 2026)**: clear to register in UK and US classes
  9, 41, 42, 44. Two unrelated "SATYS" marks belong to a French aerospace group
  (Satys SAS). No live "SATIS" marks in the relevant classes.
- **Known connotations**: mild "sadist" mishearing risk; "Satis" is also a
  Japanese smart toilet brand (INAX). Neither a blocker — flag for copywriting.
- See `CLAUDE.md` for the full list of names that were ruled out
  (Hale / Hone / Tend / Mettle / Sound / Keel / Trim / Ample / Hearth).

---

## Logo System (locked)

### Typography (logo)
- **Literata** is the single brand serif — the wordmark, mark, headings, voice,
  and nav all speak in one face. Playfair Display and Cormorant Garamond were
  explored for the wordmark but **retired** in favour of a unified single-serif
  identity (see history in `satis-wordmark-literata.html`).
- This means the logo shares DNA directly with the reading experience, and the
  brand loads one fewer font family.

### Typography (app)
- **Literata** (serif) — Coach text, Doc text, all headings, and nav labels.
  The warm, dyslexia-friendly "voice + structure" face. Open-licence (SIL OFL),
  self-hosted. Chosen as an open analogue to Claude's reading serif.
- **System sans** — everything else: body copy, data, uppercase labels, forms,
  buttons. The device's native UI font (free, instant, native feel).
- **All numerals are Literata, always** — every digit renders in Literata even
  inside system-font text, so data quietly draws the eye. Implemented via a
  digit-only `unicode-range` @font-face (no per-number markup).
- Full spec in `SATIS_DESIGN_SYSTEM.md` §2.

### Wordmark (primary lockup)
- **"Satis."** — title case, **Literata 600**, with a **full stop**.
- The full stop is load-bearing: *Satis.* reads as "enough. full stop" — the
  brand thesis compressed into the mark. It also gives the wordmark a definite
  end that balances the underline at the start.
- Letter-spacing **8px** at display size (≈0.15em at 52px) — refined, not airy.
- A **hairline keyline under the leading "S"**, **centred** on the S,
  **64% of the S's width**, sitting close beneath it (~half the earlier gap).
  This is the brand's underline motif, carried from logo into UI (nav active
  state, etc.).
- The wordmark *is* the lockup — no separate icon beside it (avoids the
  "S + Satis" doubling).

### Mark (app icon)
- A single **Literata 600 capital "S"** with the same horizontal hairline
  beneath it — **60% of the S's width**, centred.
- The S + hairline are centred together as a unit (`padding-bottom` + absolute
  positioning compensate for the font's natural top whitespace).
- Title case is for the wordmark only; the square icon uses the lone capital S.

### Container (app icon)
- Rounded square, `border-radius: ~22%` of container width.
- **Primary app icon**: sage `#88aa99` container / forest `#0e1c14` mark (inverted).
- **Alternate app icon**: forest `#0e1c14` container / sage `#88aa99` mark.
- Used for app icons; the wordmark sits outside any container.

---

## Colour Palette (locked)

### Primary
| Token | Hex | Role |
|-------|-----|------|
| Brand sage | `#88aa99` | Logo, brand colour, active/selected states, primary CTAs |
| Success green | `#2fce85` | **Reward colour** — check marks, completions, targets/goals hit, PR badges, streaks. Vibrant by design; used only at the moment of a win. Sage's hue, saturation turned up. Text/icons on it: `#06281a`. |

### Forest greens (surfaces)
| Token | Hex | Role |
|-------|-----|------|
| Page deepest | `#0a1410` | Page background |
| Surface primary | `#0e1c14` | Card surfaces, icon containers |
| Card elevated | `#111f17` | Elevated card backgrounds |
| Border subtle | `#1c2e22` | Borders, dividers |
| Surface modal | `#243a2c` | Modals, popovers, highest elevation |

### Accent forests (UI interest)
| Token | Hex | Role |
|-------|-----|------|
| Forest accent | `#163020` | Subtle elevated panels |
| Forest panel | `#1d4029` | Accent panels (hero cards, focus surfaces) |
| Forest hero | `#244e34` | Hero areas |
| Forest bright | `#2c5b3d` | Chart data, bright accents |

### Secondary accent palette (nature-inspired)
| Token | Hex | Role |
|-------|-----|------|
| Clay | `#c4a087` | Warm accents |
| Moss | `#a8b572` | Positive / streaks / consistency |
| Slate | `#7a93a6` | Info / secondary metrics / cool contrast |
| Honey | `#c4a878` | Warnings / reminders / highlights |
| Clay-deep | `#b87a6d` | Errors |

### Text
| Token | Hex | Role |
|-------|-----|------|
| Text primary | `#c8ddd2` | Body text, data values, headlines |
| Text secondary | `#7a9e8a` | Meta text, labels, captions |
| Text dim | `#4a6655` | Tertiary, disabled |

### Critical usage rule
- **Default body and data text is `#c8ddd2`**, not the brand sage. Sage is
  reserved for: logo, active states, primary CTAs, and semantically "positive"
  data (streak counts, PR badges, goal-hit indicators). When sage shows up
  everywhere, it stops carrying meaning — keep it precious.
- Functional colours (clay-deep / honey / slate) carry semantic weight
  (error / warning / info). Don't use them decoratively.

See `SATIS_DESIGN_SYSTEM.md` for full role mapping and component rules.

---

## What We Explored

| Round | Description |
|-------|-------------|
| Typeface | Eight serifs at three scales (Georgia, Cormorant 600/700, Playfair, Libre Baskerville, EB Garamond, Spectral, Lora) — `satis-logos.html` §1 |
| Mixed serif system | Playfair S + Cormorant ATI exploration — §5 |
| Unified lockup | Wordmark with underline under leading S only — §6 |
| Underline shape | Six treatments — rounded vs flat vs slab vs em-dash vs tapered vs hairline — §7 |
| Hairline at scale | Tuning width and position per icon size — §8 |
| App icon proportions | Centering S + underline as a unit — §10 |
| Colour exploration | 8 candidates compared on forest backgrounds — §11–14 |
| Mobile preview | Six icon variants on simulated home screens — `satis-mobile-preview.html` |
| Expanded palette | Richer forests + accent palette — §17 |
| Charts + nav | Data viz with bright accent, four nav active-state patterns — §18 |

---

## Decisions Made (2026-06-15)

- [x] **Wordmark & brand serif** *(2026-06-17)* — **DECIDED**: the wordmark is
  **"Satis."** in **Literata 600**, title case, with a full stop, 8px tracking,
  centred 64% keyline under the leading S. The app-icon mark is a single
  **Literata 600 "S"** + 60% keyline. **Playfair Display and Cormorant Garamond
  are retired entirely** — Satis is now a single-serif identity (Literata for
  wordmark, mark, headings, voice, nav). Study: `satis-wordmark-literata.html`.
- [x] **Wordmark underline width** — **CONFIRMED**: H2-style, 60% of leading S
  width, matches the icon.
- [x] **Icon primary** — **FLIPPED**: the **inverted** lockup (sage `#88aa99`
  container / forest `#0e1c14` mark) is now **primary**. The dark forest
  container (`#0e1c14` bg / `#88aa99` mark) is the **alternate**.
- [x] **Font loading strategy** — **Self-host Literata** as WOFF2 with
  `font-display: swap` (plus a tiny digit-only subset for the numerals
  `unicode-range` trick). Rationale: the PWA is offline-first; relying on Google
  Fonts CDN breaks text when offline and adds a render-blocking third-party
  request. Only one serif family to load now that Playfair/Cormorant are retired.
  See `SATIS_DESIGN_SYSTEM.md`.
- [x] **Tailwind theme** — **CSS variables consumed by Tailwind tokens**. Define
  the palette as CSS custom properties on `:root` (single source of truth,
  themeable), then reference them in `tailwind.config` `theme.extend.colors` via
  `rgb(var(--token) / <alpha-value>)`. Keeps the existing OLED-variable approach
  while giving utility-class ergonomics. See `SATIS_DESIGN_SYSTEM.md`.
- [x] **Repo / URL** — **Keep** `github.com/SpitefulGrain40/Pump` and the
  existing GitHub Pages URL for now. No migration. localStorage keys stay
  `pump-*` for backwards compatibility regardless.

## Open Decisions

- [x] **Bottom-nav active-state pattern** — **DECIDED**: real Lucide icons
  (Home / Food / Schedule / Doc=`Brain` / More), active state = icon + label +
  **1.5px cream keyline under the word at 44% cell width**. Cream not sage, so
  the brand colour stays reserved; three cues (colour + weight + keyline) satisfy
  WCAG. Full spec in `SATIS_DESIGN_SYSTEM.md` §4.3. Mockups in
  `satis-nav-mockups.html`. *(Keyline width 44% — confirm on hardware; option to
  switch to word-width tracking if fixed % looks off under longer labels.)*

---

## Files

| File | Purpose |
|------|---------|
| `satis-logos.html` | Workshop file — every iteration that led here, scroll to bottom for the locked brand sheet (§16) |
| `satis-mobile-preview.html` | Mobile-first mockup for testing icons against real home-screen apps |
| `SATIS_DESIGN_SYSTEM.md` | Operational design system — colour roles, component patterns, charts, nav, etc. |
| `SATIS_REBRAND_CHECKLIST.md` | Implementation checklist for the codebase rebrand |
| `CLAUDE.md` (project root) | Full technical reference for the codebase |
| `HALE_REBRAND.md` | Previous naming round (archived for context) |

---

## Next Steps When You Pick Up

1. Read `SATIS_DESIGN_SYSTEM.md` for the operational rules
2. Work through `SATIS_REBRAND_CHECKLIST.md` to update the codebase
3. Generate production PWA icons from the SVG mark (use the
   `web-asset-generator` skill or `Sharp` at 48/96/192/512px in both dark
   and inverted variants)
4. Update `manifest.json` with new `name`, `short_name`, `icons`, `theme_color`
5. Update `index.html` `<title>` and meta tags
6. Update `package.json` `name`
7. Sweep in-app strings — `useUserProfile`, `Coach.jsx`, `Doc.jsx`, etc. for
   "Pump" references (UI strings; not localStorage keys, which stay
   `pump-*` for backwards compatibility — see Checklist for the rule)
8. Update Tailwind theme / CSS variables with the new palette
9. Test deploy via `npm run deploy:test` before promoting to production

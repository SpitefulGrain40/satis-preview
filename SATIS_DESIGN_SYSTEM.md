# Satis — Design System

Operational UI rules for the Satis app. This is a **living document** — open it
during implementation. For the brand story, name rationale, and logo
construction see `SATIS_REBRAND.md`. For the codebase rebrand task list see
`SATIS_REBRAND_CHECKLIST.md`.

> **Visual companion:** `satis-design-system.html` renders every token and
> component in this doc as a live, interactive styleguide. Use it to *see* the
> system; use this markdown for the precise spec. **Keep the two in sync** — when
> a value changes here, update the HTML (and vice versa).

**Guiding principle:** *calm confidence*. Restraint over loudness. The brand
colour is precious — it signals, it doesn't decorate.

---

## 1. Colour

### 1.1 Tokens

Defined once as CSS custom properties on `:root`, consumed by Tailwind via
`rgb(var(--token) / <alpha-value>)`. Single source of truth.

```css
:root {
  /* Brand */
  --sage:          136 170 153;  /* #88aa99 — brand, primary accent */

  /* Reward — vibrant success green (reserved for wins) */
  --success:        47 206 133;  /* #2fce85 — completions, checks, targets hit */
  --on-success:      6  40  26;  /* #06281a — text/icons on a --success fill */

  /* Forest surfaces (low → high elevation) */
  --page:          10 20 16;     /* #0a1410 — app background */
  --surface:       14 28 20;     /* #0e1c14 — cards, icon containers */
  --card:          17 31 23;     /* #111f17 — elevated cards */
  --border:        28 46 34;     /* #1c2e22 — borders, dividers */
  --modal:         36 58 44;     /* #243a2c — modals, popovers */

  /* Accent forests (UI interest, charts) */
  --forest-accent: 22 48 32;     /* #163020 — subtle elevated panel */
  --forest-panel:  29 64 41;     /* #1d4029 — accent / focus surfaces */
  --forest-hero:   36 78 52;     /* #244e34 — hero areas */
  --forest-bright: 44 91 61;     /* #2c5b3d — chart data, bright accent */

  /* Secondary accents (nature palette) */
  --clay:          196 160 135;  /* #c4a087 — warm accents */
  --moss:          168 181 114;  /* #a8b572 — secondary accent / variety */
  --slate:         122 147 166;  /* #7a93a6 — info / secondary metrics */
  --honey:         196 168 120;  /* #c4a878 — warning / reminders */
  --clay-deep:     184 122 109;  /* #b87a6d — error */

  /* Text */
  --t-primary:     200 221 210;  /* #c8ddd2 — body, data, headlines */
  --t-secondary:   122 158 138;  /* #7a9e8a — meta, labels, captions */
  --t-dim:          74 102  85;  /* #4a6655 — tertiary, disabled */
}
```

### 1.2 The reserved-colour rule (most important rule in this doc)

**Default text and data is `--t-primary` (cream), NOT sage.**

Two greens, two jobs — keep them distinct:

- **Sage (`--sage`)** = the **brand**. Reserved for: the logo/wordmark, active /
  selected states (where not handled by the cream keyline — see nav), and
  primary CTA buttons.
- **Success (`--success`, vibrant `#2fce85`)** = the **reward**. Reserved for the
  moment of a win: check marks, completions, "done" states, targets/goals hit,
  PR badges, streak milestones, a fully-met progress fill. Brighter than sage on
  purpose — the tick should feel satisfying.

Why two: sage is calm and ever-present (brand); the success green is rare and
energising (reward). If a win used sage it wouldn't pop; if success green were
used decoratively it would stop signalling achievement. A kcal number is just
data → cream. A kcal number that means "goal hit" → success green. Keep both
precious.

### 1.3 Semantic colour roles

| Role | Token | Use |
|------|-------|-----|
| Success / win | `--success` (`#2fce85`) | Check marks, completions, targets/goals hit, PR badges, streak milestones, full progress fills. The reward colour — used only at the moment of achievement. |
| Brand / active | `--sage` | Logo, active/selected state, primary CTA. Calm and ambient — not a "win" signal. |
| Warning / attention | `--honey` | Reminders, "due" states, soft nudges. Never alarming. |
| Error / destructive | `--clay-deep` | Validation errors, destructive confirms. Muted by design — we don't shout. |
| Info / neutral data | `--slate` | Secondary metrics, trend lines, "for reference" stats. Cool contrast to the warm greens. |
| Decorative interest | `--forest-*`, `--clay` | Accent panel backgrounds, chart fills. Carries no semantic weight. |

### 1.4 Contrast (WCAG)

All combinations below are verified against the surface they sit on:

| Foreground | On surface | Ratio | Verdict |
|-----------|-----------|-------|---------|
| `--t-primary` | `--surface` | ~11:1 | AAA |
| `--t-secondary` | `--surface` | ~5.1:1 | AA (use ≥ small-bold or ≥18px) |
| `--sage` | `--surface` | ~7:1 | AAA |
| `--success` | `--surface` | ~9:1 | AAA |
| `--on-success` | `--success` fill | ~10:1 | AAA — dark text/checks on the green |
| `--t-dim` | `--surface` | ~2.6:1 | Decorative only — never body text |

Rule: body text uses `--t-primary`. `--t-secondary` is fine for labels/captions
but keep it ≥ 13px or semibold. `--t-dim` is for non-essential decoration
(placeholder dots, faint gridlines) — never for content a user must read.

---

## 2. Typography

### 2.1 Families — two roles (single-serif identity)

| Family | Weight | Role | Loading |
|--------|--------|------|---------|
| **Literata** | 400/500/600 | **The brand serif** — logo wordmark + mark, Coach text, Doc text, all headings, nav labels. Everywhere the brand "speaks," is named, or orients the user. | Self-hosted WOFF2 |
| **System UI stack** | 400/500/600 | **Everything else** — body copy, data, uppercase labels, captions, forms, buttons | Native |

Two jobs, cleanly separated:
- **Literata (serif)** = brand + reading + structure. The warm, dyslexia-friendly
  serif carries the wordmark ("Satis."), the app-icon S, conversation (Coach/Doc),
  headings, and nav labels. One face ties the logo directly to the reading
  experience — a single-serif identity. (Playfair Display and Cormorant Garamond
  were explored for the wordmark and **retired**.)
- **System sans** = interface. Everything functional and dense — the device's
  native UI font (`-apple-system, BlinkMacSystemFont, "Segoe UI", system-ui,
  sans-serif`). Free, instant, native feel.

**All numerals are Literata — always.** Every digit renders in Literata
regardless of the surrounding text's font, including inside system-sans body,
labels, captions, badges, and charts. This makes data the visual hero — numbers
carry a quiet serif weight that draws the eye, which is the whole point of a
tracking app.

Implement with a **digit-only `unicode-range` @font-face** layered ahead of the
system stack, so no per-number markup is ever needed:

```css
@font-face {
  font-family: 'LiterataNum';
  src: url('/fonts/literata-subset.woff2') format('woff2');
  /* digits + comma, period, thin space, percent for "2,184" "102.4" "98%" */
  unicode-range: U+0030-0039, U+002C, U+002E, U+0025, U+2009;
  font-display: swap;
}
:root {
  --sys: 'LiterataNum', -apple-system, BlinkMacSystemFont, 'Segoe UI',
         system-ui, sans-serif;
}
```

Because the digit-only face is listed first, digits resolve to Literata and
every other glyph falls through to the system font automatically. Subset the
Literata WOFF2 to just those codepoints to keep it tiny.

**Font loading:** self-host **Literata** as a Latin-subset WOFF2 with
`font-display: swap`, plus the tiny digit-only subset above for the numerals
trick. The PWA is offline-first; a Google Fonts CDN dependency breaks text
offline and adds render-blocking requests. Only one serif family to load —
Playfair/Cormorant are retired.

### 2.2 Type scale

Font column: **L** = Literata, **Sys** = system sans.

| Token | Font | Size / line-height | Weight | Use |
|-------|------|-------------------|--------|-----|
| `display` | L | 32 / 38 | 600 | Hero numbers / figures (kcal, weight) |
| `title` | L | 22 / 28 | 600 | Screen titles |
| `heading` | L | 17 / 24 | 600 | Card / section headings |
| `read` | L | 17 / 1.65 | 400–500 | Coach &amp; Doc conversation text |
| `nav` | L | 11 / 14 | 500 | Bottom-nav labels |
| `body` | Sys | 15 / 22 | 400 | Default UI text |
| `body-sm` | Sys | 13 / 18 | 400 | Secondary UI text |
| `label` | Sys | 11 / 14 | 500 | Uppercase eyebrows, `letter-spacing: 1.5px` |
| `caption` | Sys | 10 / 14 | 500 | Meta, timestamps |

Uppercase labels (the `label` token) stay **system sans** with
`letter-spacing: 1.5–2px` and `text-transform: uppercase`. The serif/sans
contrast — Literata heading over a sans eyebrow — is a deliberate texture.

Note the "Sys" rows above set their **letters** in system sans, but their
**digits** still render in Literata via the rule above — e.g. a `caption` like
"Updated 2 min ago" has a serif "2" inside system-font words.

---

## 3. Spacing, radius, elevation

**Spacing scale (4px base):** 4, 8, 12, 16, 20, 24, 32, 40, 48, 64.
Card padding default 16–18px. Screen gutters 16px. Gap between cards 12–14px.

**Radius:**
| Token | Value | Use |
|-------|-------|-----|
| `r-sm` | 6px | Chips, small controls, inline icons |
| `r-md` | 12px | Cards, buttons, inputs |
| `r-lg` | 16–20px | Sheets, nav bar, modals |
| `r-icon` | 22% of size | App icon container (matches the brand mark) |

**Elevation** is expressed by surface colour, not shadows (OLED dark theme).
Going up the stack: `--page` → `--surface` → `--card` → `--modal`. Borders
(`--border`) separate same-level surfaces. Use shadow only for true overlays
(modal scrim, dropdown) and keep it soft: `0 8px 30px rgba(0,0,0,0.4)`.

---

## 4. Components

### 4.1 Cards
- Background `--card`, 1px `--border`, radius `r-md`, padding 16–18px.
- Uppercase `label` token (system sans) for the eyebrow; `display`/`heading`
  (Literata) for the value/title.
- Data values default to `--t-primary`; only sage when semantically positive.
- Accent/hero cards may use `--forest-panel` background to draw the eye —
  use sparingly (one per screen max).

### 4.2 Buttons
| Variant | Fill | Text | Use |
|---------|------|------|-----|
| Primary | `--sage` | `--page` (dark) | The one main action per screen |
| Secondary | transparent, 1px `--border` | `--t-primary` | Secondary actions |
| Ghost | none | `--t-secondary` | Tertiary / low-emphasis |
| Destructive | transparent, 1px `--clay-deep` | `--clay-deep` | Delete/remove |

- Min height 44px. Radius `r-md`. Label weight 600.
- One primary button per screen — if everything is primary, nothing is.

### 4.3 Bottom navigation (LOCKED spec)

**Structure:** 5 persistent top-level tabs — Home, Food, Schedule, Doc, More.
Icon (Lucide) above a **Literata label** (`nav` token, ~11px). Same order, same
place, every screen.

**Icons (Lucide React):**
| Tab | Component |
|-----|-----------|
| Home | `Home` |
| Food | `UtensilsCrossed` (or a bowl glyph) |
| Schedule | `CalendarDays` |
| Doc | `Brain` |
| More | `Menu` or `Ellipsis` |

**Active state — the cream-keyline pattern:**
- Active icon + label: `--t-primary` (cream), label weight 600
- A **1.5px cream keyline under the label**, **44% of the tab cell width**,
  centred, radius 1px
- Inactive icon + label: `--t-secondary` (muted), weight 400
- The keyline is the brand's underline motif carried from the logo into the UI

**Why cream not sage:** keeps sage reserved (§1.2), and the active state still
carries **three** distinguishing cues — colour (cream vs muted), weight (600 vs
400), and the keyline — so it satisfies "don't rely on colour alone" (WCAG 1.4.1)
without shouting.

**Interaction & accessibility:**
- **Touch target:** the full tab cell is tappable and ≥48×48px — not just the
  23px icon. Pad the cell, don't rely on the glyph.
- **Cue redundancy:** never reduce the active state to a single cue. If the
  keyline is ever dropped in a constrained context, the colour+weight shift must
  remain.
- **Keyline floor:** 44% width × 1.5px is the minimum. Don't go thinner/shorter
  or the colour shift becomes the only reliable cue (fails for colourblind users
  and in glare).
- **Tap active tab again:** returns to the top of that tab's stack / resets scroll.
- **Reduced motion:** the keyline grow/fade transition (`width .15s`) must be
  disabled under `prefers-reduced-motion: reduce` — snap to state instantly.
- **Semantics:** `role="tablist"` on the bar, `role="tab"` + `aria-selected`
  on each, `aria-label` on icon-bearing controls. The active tab gets
  `aria-current="page"`.
- **Safe area:** pad the bar for the iOS home indicator
  (`padding-bottom: env(safe-area-inset-bottom)`).

### 4.4 Charts

Two colouring modes, kept distinct:

**1. State colouring** — one metric against its target, per data point:
- **Below target** follows the progress ramp: `--sage` (≤60%), `--honey` (61–90%).
- **Met** days rest in calm `--forest-bright` (the steady baseline) — *not*
  vibrant success.
- **`--success` is spent sparingly** — only a genuine standout (the week's best /
  a new PR), never on every bar that cleared the line. Flooding a chart with the
  reward green makes it meaningless and loud (same discipline as §1.2).
- A ceiling metric over its cap can use `--clay-deep`.

So honey/sage flag the shortfalls, forest-green is the baseline, and one bright
bar is the win. (Note: a single live progress *bar/ring* uses the full ramp incl.
vibrant success at 91–100%, per §4.8 — that's one element, not a field of bars.)

**2. Series colouring** — telling multiple metrics/lines apart. Uses a subtle
**series palette**, ordered:

| Order | Token | Suggested metric |
|-------|-------|------------------|
| 1 | `--forest-bright` (green) | steps / activity / generic primary |
| 2 | `--slate` | weight |
| 3 | `--moss` | lean mass |
| 4 | `--clay` | body-fat |

The series palette **deliberately excludes `--honey` and `--clay-deep`** — those
carry state/alert meaning, so series identity never collides with goal state.
Metrics usually shown against a target (calories, protein) use state colouring
instead. Keep a consistent metric→colour mapping across the whole app.

**Legibility rules (both modes):**
- Lines ≥ 2.5px; distinguish series by **hue, never lightness alone** (fails on
  dark and for colour-blindness).
- **Label series directly** at the line end — avoid separate legends.
- Gridlines faint: `--border`, 1px, dashed.
- Emphasise the most-recent / "now" point with a filled dot.
- Axis labels `--t-dim`, caption size; letters system sans, **digits Literata**
  (§2), including axis figures.
- Max ~4 series; beyond that use small multiples.

### 4.5 Badges & chips
- Pill, radius `r-sm`, `padding: 3px 8px`, caption size, `letter-spacing: 0.5px`.
- Semantic tint pattern: `color: <role>`, `background: <role>/12–14%`,
  `border: 1px <role>/25–30%`. E.g. a "NEW PR" badge = `--success` text on a
  success-14% fill; a "DUE" badge = `--honey`; "RESTING" = `--slate`.

### 4.6 Inputs
- Background `--surface`, 1px `--border`, radius `r-md`, text `--t-primary`.
- Focus: border → `--sage`, no harsh glow (subtle is on-brand).
- Placeholder `--t-dim`. Labels above the field in the `label` token.
- Error: border → `--clay-deep`, message below in `--clay-deep` body-sm.

### 4.7 Modals / sheets
- Bottom sheets for mobile actions; anchor `absolute bottom-0`, `max-height: 85dvh`.
- Surface `--modal`, radius `r-lg` top corners, soft scrim
  `rgba(0,0,0,0.5)` behind.
- Keep primary action visible above the keyboard (fixed action row).

### 4.8 Success & completion states
`--success` (`#2fce85`) is applied in **tiers by the size of the win**, and only
at a moment of achievement — never decoratively. The governing distinction:
**sage = "in progress / on track"; success green = "done / hit."**

| Scenario | Treatment |
|----------|-----------|
| Completed item / check | Filled `--success` circle (≈24px) + dark check in `--on-success`. Checklists, done sessions, ticked tasks. |
| Goal / target hit (prominent) | Filled success **card** — `--success` background, `--on-success` text/number. |
| Goal hit (compact) | Success-green eyebrow + value, or a success **badge** (`--success` text on success-14% fill). |
| PR / streak milestone | Success green **+ soft glow** (`box-shadow: 0 0 24px rgba(47,206,133,0.28)`), typically on a `--forest-bright` card. Reserved for rare milestones so the glow keeps its impact. |
| Inline positive | Success-green **text** inline (e.g. "on target ✓"). |
| Progress fill / ring | **Graduated** — see below. |

Discipline: if success green shows up when nothing was achieved, it stops
signalling achievement. Keep it to the moment of the win. Checks/icons on a
`--success` fill use `--on-success` (`#06281a`) for ~10:1 contrast.

**Graduated progress fills.** A bar/ring changes colour by proximity to target,
so a glance reads where you stand:

| % of target | Colour |
|-------------|--------|
| 0–60% | `--sage` |
| 61–90% | `--honey` |
| 91–100% | `--success` |

**Over-target behaviour depends on the metric type:**
- **Ceiling metrics** (you don't want to exceed — e.g. **calories**): 100–105%
  stays `--success` (a tolerance band); **> 105% → `--clay-deep`** (red — over
  the cap).
- **Floor / more-is-better metrics** (you want *at least* X — e.g. **protein**):
  **above 100% stays `--success`** — overshooting is good, never red.

Each metric declares its type (ceiling vs floor) so the bar knows how to treat
the overflow. The muted `--clay-deep` red is deliberate — it flags "over" without
shaming, per the brand's calm tone.

---

## 5. Iconography
- **Lucide React** throughout (already the app's set). Stroke 1.5–1.75px at 24px.
- Inactive nav/UI icons: `--t-secondary`. Active: `--t-primary`.
- Don't mix filled and outline styles within one surface unless filled = active.
- Inline content icons inherit text colour and sit at the optical size of the
  text they accompany.

---

## 6. Motion
- **Fast and quiet:** 120–180ms for state changes, ease-out. Nothing bouncy.
- Page/tab transitions: cross-fade or subtle slide, ≤200ms.
- The nav keyline animates width (`.15s`) — the one signature motion.
- **Always** honour `prefers-reduced-motion: reduce` — snap, don't animate.
- No decorative/looping animation. Calm confidence means stillness by default.

---

## 7. Accessibility checklist (ship gate)
- [ ] Body text `--t-primary`; `--t-secondary` only ≥13px or semibold
- [ ] No content conveyed by colour alone (≥2 cues for state)
- [ ] Interactive targets ≥44×44pt / 48×48px
- [ ] Focus states visible (sage border / outline), logical tab order
- [ ] `prefers-reduced-motion` respected everywhere
- [ ] Nav: `role=tablist/tab`, `aria-selected`, `aria-current`
- [ ] iOS safe-area insets on the bottom nav
- [ ] Dynamic type / zoom doesn't break layouts (test at 200%)

---

## 8. Quick reference — "what colour is this?"
- Plain text / number → **cream** (`--t-primary`)
- A label/caption → **muted** (`--t-secondary`)
- It's a completion / check / goal hit / PR / streak win → **success green** (`#2fce85`)
- It's a reminder / soft warning → **honey**
- It's an error → **clay-deep**
- It's a secondary/info metric or a 2nd chart series → **slate**
- It's an accent surface for visual interest → **forest-panel / forest-bright**
- The logo, the one main button, the active selection → **sage** / cream keyline

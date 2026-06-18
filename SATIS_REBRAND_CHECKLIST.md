# Satis — Rebrand Checklist

Every change to take the live app from **Pump** to **Satis**, grounded in the
actual `C:\Users\mikes\Pump` codebase. **Nothing here is executed** — it's the
plan; code changes happen only on explicit go-ahead. Visual companion:
`satis-rebrand-checklist.html` (interactive, tickable). Design rules:
`SATIS_DESIGN_SYSTEM.md`.

> **Two hard rules:**
> 1. **localStorage keys stay `pump-*`** — renaming wipes every existing user's
>    data. Change UI copy, never the keys.
> 2. **Repo & URL stay "Pump"** (decided) — `github.com/SpitefulGrain40/Pump`
>    and the Pages URL don't change. The app is *named* Satis; its address stays
>    Pump for now.

Tags: **STRING** copy · **ASSET** image/icon · **THEME** colour · **TYPE** font ·
**KEEP** leave as-is · **BUILD** build/deploy · **PHASE 2** larger, can follow.

---

## 1. Identity & metadata
- [ ] **App name → "Satis"** `STRING` — `name` ("Pump - AI Fitness Coach") and
  `short_name` ("Pump"). Files: `manifest.json`, `public/manifest.json`
- [ ] **Manifest description** `STRING` — rewrite to Satis positioning (calm,
  sustainable progress; not "weight loss / fitness coach").
- [ ] **Manifest theme + background colour** `THEME` — currently OLED black
  `#000000`. → `background_color #0a1410`, `theme_color #0e1c14`.
- [ ] **Page `<title>`** `STRING` — `index.html`, `index.src.html`
- [ ] **HTML theme/background meta** `THEME` — `theme-color` / `background-color`
  `#000000` → forest.
- [ ] **App-title / application-name meta** `STRING` — `apple-mobile-web-app-title`,
  `application-name` "Pump" → "Satis".
- [ ] **HTML meta description** `STRING`
- [ ] **package.json name** `STRING` — `"pump"` → `"satis"` (cosmetic, private).
- [ ] **README + USER_GUIDE branding** `STRING`

## 2. Icons & favicons
Primary = inverted (sage container, forest S). Source SVGs in `logo/`.
- [ ] **Replace `icon.svg`** `ASSET` — Satis S-mark (from `logo/satis-icon-primary-outlined.svg`).
- [ ] **Regenerate `icon-192.png` / `icon-512.png`** `ASSET` — any + maskable;
  maskable copies need safe-zone padding (mark within inner ~80%).
- [ ] **apple-touch-icon** `ASSET` — regenerates with the 192 PNG.
- [ ] **Confirm icon orientation** `KEEP` — primary inverted; dark/alt available
  for an adaptive variant.

## 3. Typography
- [ ] **Self-host Literata (woff2)** `TYPE` — 400/500/600, `@font-face`,
  `font-display:swap`. No CDN (offline-first). `src/index.css`, `public/fonts/`
- [ ] **Numerals unicode-range** `TYPE` — digit-only "LitNum" face ahead of the
  system stack so all numbers render Literata. `src/index.css`
- [ ] **Apply Literata** `TYPE` `PHASE 2` — Coach/Doc/headings/nav; system sans
  elsewhere. `src/components/`

## 4. Colour & theme (in-app)
- [ ] **Add Satis palette tokens** `THEME` — design-system CSS variables. `src/index.css`
- [ ] **Migrate UI surfaces to forest palette** `THEME` `PHASE 2` — OLED black →
  forest ladder. Significant; own phase.
- [ ] **Success / progress colour rules** `THEME` `PHASE 2` — graduated fills
  (sage→honey→success, red over a kcal cap); reserved success green.
  `Progress.jsx`, `Dashboard.jsx`

## 5. In-app strings
- [ ] **UI copy "Pump" → "Satis"** `STRING` — `OnboardingWizard.jsx`,
  `Settings.jsx`, `Coach.jsx`, `Doc.jsx`, etc.
- [ ] **AI prompt app-name** `STRING` — Coach/Doc system prompts. `src/services/ai/context.js`
- [ ] **Do NOT rename localStorage keys** `KEEP` — all `pump-*` keys stay. `src/hooks/`
- [ ] **Code identifiers / cache prefix / dev script names** `KEEP` `PHASE 2` —
  cosmetic, optional later.

## 6. Service worker & deploy
- [ ] **SW cache name** `BUILD` — stamped `pump-YYYYMMDD-HHMMSS`; optionally
  switch prefix to `satis-` (forces clean refresh). `public/sw.js`, `sw.js`
- [ ] **Deploy scripts** `BUILD` — stamp string if prefix changes.
  `scripts/deploy.cjs`, `scripts/deploy-test.cjs`
- [ ] **Dev tooling names** `PHASE 2` — `pump-cli-proxy.cjs`, `/pump-dev`,
  `/pump-test`. Optional.

## 7. Build, verify & document
- [ ] **Build** `BUILD` — `npm run build`
- [ ] **Deploy to test + approve** `BUILD` — `npm run deploy:test` → preview →
  confirm before production.
- [ ] **Production deploy + push** `BUILD` — `node scripts/deploy.cjs`, commit
  `docs/`, push.
- [ ] **Update CLAUDE.md** `BUILD` — record the rebrand.

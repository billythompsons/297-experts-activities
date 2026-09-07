# SANITY-SPEC.md - the checkable design spec for all 501 BostonDeveloper surfaces
> Source: live measurement of sanity.io (homepage + /pricing) via browser on 2026-09-07, desktop 1280px and 380px viewports, cross-checked against their 324KB global stylesheet. The narrative teardown is SANITY-TEARDOWN.md (same repo). This file is the enforceable contract: every value below is a checkable rule. Folk is retired as the bar; anything still folk-styled is legacy pending restyle.
> Ethan rule: free/open-source assets only; products look like a design team built them.

## 0. Font loading (open-license stand-ins)
Waldenburg is proprietary. Open stand-ins (both OFL, Google Fonts):
- Sans/display: **"Inter Tight"** (400, 500; ital off) - closest metric/character match to Waldenburg's neo-grotesk.
- Mono: **"IBM Plex Mono"** (400) - same family sanity uses.
```css
@import url('https://fonts.googleapis.com/css2?family=Inter+Tight:wght@400;500&family=IBM+Plex+Mono&display=swap');
```

## 1. Tokens (exact)
```css
:root{
  --font-sans:"Inter Tight",ui-sans-serif,system-ui,sans-serif;
  --font-mono:"IBM Plex Mono",ui-monospace,monospace;
  --black:#0b0b0b; --white:#ffffff;
  --gray-100:#ededed; --gray-200:#d6d6d6; --gray-300:#b9b9b9; --gray-500:#797979;
  --gray-700:#4a4a4a; --gray-800:#353535; --gray-900:#212121;
  --brand:#ff560a;                    /* one hot orange; max 1 use per view */
  --blue:#0084f8; --blue-700:#0052ef; --blue-100:#afe3ff;
  --green:#00fe00; --magenta:#ff23fc; --yellow:#fdfe00;  /* full-bleed blocks only, never tints */
  --bg:var(--black); --fg:var(--white);                 /* DARK is the default surface (sanity ships dark-first) */
  --bg-inv:var(--white); --fg-inv:var(--black);
  --bg-dim:var(--gray-900);           /* dark-dim; light-dim = --gray-100 */
  --hair:rgba(255,255,255,.18);       /* 1px hairline on dark; on light: var(--gray-200) */
  --radius:0; --radius-pill:99999px;  /* BINARY: sharp or pill. No other radius. */
}
```

## 2. Typography rules (checkable)
| Role | Font | Size/lh | Weight | Tracking | Transform |
|---|---|---|---|---|---|
| Display (popup title) | sans | 28px/1.0 (measured scale-down of 60px h1 at 380px) | 400 | -0.04em (-1.12px) | none |
| Section heading | sans | 20px/1.1 | 400 | -0.01em (-0.2px) | none |
| Body | sans | 15px/1.5 | 400 | 0 | none |
| Eyebrow / label | mono | 11-13px/1.3 | 400 | 0 | UPPERCASE |
| Button text | mono | 13px/1.3 | 400 | 0 | UPPERCASE |
| Stats / prices / numbers | mono | 13-20px | 400 | 0 | none |
Rules: headings NEVER bold (400; 500 allowed only for a single emphasized inline word - replaces folk's serif-italic accent). No exclamation marks in UI copy. Headings are declarative claims ("Track every cron job"), proof rows carry numbers ("297 features, 1 place").

## 3. Surfaces
- Default view: `--bg` (#0b0b0b), `--fg` white text.
- Section rhythm comes from full-bleed flips: dark -> dim (#212121) -> white inverse block -> (rare) saturated accent block. NOT from cards.
- No border-radius except pills. No box-shadows (0 allowed). Borders: 1px `--hair`.
- Section padding: 24-32px vertical in popups (sanity uses 48/96/128 at desktop; scale = /4).

## 4. Components
- **Button primary**: pill radius, 1px border, inverse block (on dark: white bg, #0b0b0b text; on light: black bg, white text). Mono uppercase 13px. Padding 8px 16px; min-height 32px. Hover swaps fg/bg (150ms).
- **Button ghost**: same text style, no border, transparent bg, padding 4px 12px.
- **Button accent**: pill, `--blue-700` (#0052ef) bg + border, white text. (Sanity's measured accent button is blue, not orange; orange is reserved for brand marks and ONE highlight per view.)
- **Chip/tag**: pill, 1px `--hair` border, mono uppercase 11px, padding 4px 8px.
- **Input**: radius 0, 1px `--hair` border, transparent bg, sans 15px; focus = 2px dotted outline, 2px offset.
- **List rows / cards**: radius 0, flat, separated by 1px hairlines; selected state = inverse block, not a tint.
- **Tier chips (Free/Starter/Pro/Accelerator/Studio)**: pill chip per above; paid tiers may use accent-block backgrounds (blue/green/magenta/yellow at full saturation, black mono text).

## 5. Motion
- Only `color, background-color, border-color` transitions, 150ms ease. No transforms, no keyframes, no shadows animating.

## 6. Layout (380px popup)
- Side padding 16px; content max-width = viewport minus 32px.
- 4px base gutter unit (sanity --gutter:4px); spacing scale 4/8/12/16/20/24/32/48/64.
- One idea per view. Hierarchy via size + whitespace, never via decoration.

## 7. Art / iconography
- Icons: 1px-stroke line icons (their art is stroke-based line illustration + duotone blocks), depicting what the product DOES (Ethan rule). No emoji-as-icon, no stock 3D.
- Accent blocks may carry big mono numerals/labels.

## 8. Copy voice
- Declarative, quantified, no exclamation. Examples on-bar: "One API, every platform", "Enterprise-grade everything", "Less talk, more code".
- Feature bullets: noun-first fragments ("Real-time collaboration", "99.99% uptime SLA").

## 9. Restyle gate (per surface)
1. Tokens from section 1 replace folk vars. 2. Type table from section 2 applied. 3. Radius audit: only 0/pill. 4. Shadow audit: none. 5. Buttons/chips per section 4. 6. Dark-first surface. 7. 380px screenshot verify (push + screenshot loop) before ship.

# SANITY-TEARDOWN - why sanity.io's design language is the new bar (and how folk loses to it, element by element)

> Ethan's standing rule: every product must look like a design team built it. On 2026-09-06 the design bar moved from folk.com to sanity.io. This teardown is the evidence pack: real values pulled from sanity.io's live stylesheets, element by element, each with WHAT / WHY / how it beats our current folk bar. Tonight's browser run (post-midnight budget reset) verifies every pixel value live and folds the result into SANITY-SPEC.md, the checkable spec all 501 surfaces get restyled against.

**Evidence base (this teardown, no browser):**
- https://www.sanity.io/ homepage HTML (385 KB) + its global stylesheet `/_astro/global.DHS71LkH.css` (324 KB) - every token quoted below is read from that CSS, not guessed.
- https://www.sanity.io/pricing (404 KB) - interior-page component/copy evidence.
- Folk values read from our own chassis `folk.css` (the bar being replaced).

---

## 1. Typography - one grotesk, one mono, zero decoration

**WHAT (real values):**
- Sans: `Waldenburg` (Sanity's custom grotesk), only 3 faces ship: 400, 400 italic, 600. Fallback is Arial with metric overrides (`size-adjust:105.2%; ascent-override:91.16%; descent-override:23.29%`) so the fallback is layout-identical and the page never shifts while fonts load.
- Mono: `IBM Plex Mono` (400 + 400 italic) - a real system voice, not an afterthought.
- Headings: **weight 400, never bold.** Confidence comes from scale and tracking: `letter-spacing:-0.04em`, `font-feature-settings:"ss07","cv01","cv11","cv12","cv13"`, `text-box:trim-both cap alphabetic` (optically trimmed line boxes). Hero h1 ramps 60px → 72px (≥400px) → 96px (md) → 112px (lg), line-height 1.05→1, `text-wrap:balance`.
- Body: sans 400, quiet.
- Eyebrows, buttons, labels: **mono, uppercase, 13px (0.8125rem), weight 400, letter-spacing 0.**

**WHY it works:** one typeface does all the voice; weight is flat so size and tracking carry hierarchy. Mono uppercase microcopy adds engineering texture - it reads like a tool built by people who ship. The metric-matched Arial fallback means the design is stable even before fonts arrive: discipline you can feel.

**Beats folk:** folk borrows decoration - a serif italic accent span inside an otherwise plain Inter line (`hero-line` 22px/500/-0.02em). It's one nice gesture that everything else leans on. Sanity needs no gesture: 112px of -0.04em grotesk at weight 400 is the gesture. Two type voices (sans + mono) with strict roles also scales across 501 products better than "put a serif italic on the important word."

---

## 2. Color - black, white, one brand orange, four loud accents

**WHAT (real values):**
- Base: `--color-black:#0b0b0b`, `--color-white:#fff`. True dark-mode inversion built in (`--color-bg-base` = white/black, `--color-bg-inverse-base` = black/white, `--color-bg-dim` = gray-100/gray-900).
- Brand: `#ff560a` (display-p3 `1 .3333 0`) - one hot orange, used once per screen max.
- Grays: 100 `#ededed` / 200 `#d6d6d6` / 300 `#b9b9b9` / 500 `#797979` / 700 `#4a4a4a` / 800 `#353535` / 900 `#212121`.
- Accents (each with 100/300/500/700 steps + P3 variants): blue `#0084f8` family, green `#00fe00` family, magenta `#ff23fc` family, yellow `#fdfe00` family. Used as full-bleed blocks, not tints.
- Borders: 1px `var(--color-border-dim)` hairlines.

**WHY it works:** the page is monochrome until it isn't - when the orange or a raw `#00fe00` block appears, it lands like a siren because nothing else competes. Saturated accents on flat fields read confident and modern; tints read timid.

**Beats folk:** folk's palette is warm pastels on warm paper (`--paper:#faf7f1`, butter `#fbe8a6`, powder `#d7e6fb`, mint `#d9efdf`). Pleasant, but every surface whispers at the same volume. Sanity's restraint-then-blast dynamic gives real hierarchy of attention. Folk also has no true dark/inverse mode; sanity's token system inverts natively.

---

## 3. Surfaces & layout - flat fields, sharp rhythm, engineered grid

**WHAT (real values):**
- Grid: 12 columns, **4px gutter** (`--gutter:4px`), default content width 78rem, page max 1920px, section padding-x 1.5rem, min side margin 24px. Navbar height 67px.
- Spacing scale (rem): 2 / 4 / 6 / 8 / 12 / 16 / 20 / 24 / 32 / 40 / 48 / 64 / 80 / 96 / 128. Widget heights 25 / 35 / 45px; icon boxes 19 / 21 / 25px.
- Rhythm: full-width sections flip white → black → dim gray → saturated accent. The flip is the separator - not borders or cards.
- Elevation: essentially none. One decorative box-shadow in the entire 324 KB stylesheet (`0 0 8px 2px` glow) and one gradient. Everything else is flat color + 1px hairlines.

**WHY it works:** flatness + section flips = rhythm without furniture. No card-in-card nesting, no shadow soup. The 4px gutter makes dense 12-col layouts feel machined, not cramped.

**Beats folk:** folk is one continuous paper tone with 10px-radius cards and hairline dividers - cozy, but monotone, and the radius is doing decoration work that layout should do. Sanity gets more drama from a single white→black flip than folk gets from its whole card system.

---

## 4. Components - binary radius, mono buttons, hairline discipline

**WHAT (real values):**
- **Radius is binary: `0` (sharp) or `99999px` (pill). Nothing between.** (2 uses of 12px and one 8px exist in 324 KB of CSS; they're exceptions, not a scale.)
- Buttons: mono uppercase 13px/400, pill radius, 1px border, `text-box:trim-both` optical trim. Sizes: sm (min-height 25px, pad 4/8), md (35px, 8/12... spacing-4/spacing-12), lg (45px, 8/32). Modes: `primary` = inverse block (black bg / white text on light surfaces, flips on hover), `ghost` = borderless, `accent` = brand orange.
- Eyebrows: mono uppercase 13px, gray-500 on light.
- Focus: 2px dotted outline, 2px offset - visible without a glow.
- Motion: nearly all transitions are `color, background-color, border-color` at ~150ms ease. State changes are recolors, not animations.

**WHY it works:** every interactive element speaks the same two shapes (sharp field or pill control) and the same mono label voice. Binary radius is a decision you can see. 150ms recolors keep the UI feeling instant and honest - no physics cosplay.

**Beats folk:** folk has a radius scale (10px cards, 100px chips, mixed), serif-accent buttons, and heavier chrome. Sanity's components are fewer, stricter, and instantly recognizable. Strictness is what survives being stamped onto 501 different products.

---

## 5. Copy voice - declarative, numbered, zero exclamation

**WHAT (verbatim from the homepage):**
- H1: "The Content Operations Platform" - a category claim, no verb, no punctuation.
- H2s: "Mirror how your content operations team works" / "Content Operations without the busywork" / "Power anything. One API, every platform" / "Loved by 1M+ users and 6k+ teams" / "Enterprise-grade everything" / "Less talk, more code".
- Pricing page headlines follow the same pattern: short declaratives, proof numbers, no exclamation marks anywhere.

**WHY it works:** every headline is a claim or a proof. Numbers do persuasion ("1M+ users", "6k+ teams"). Lowercase-style confidence - no ALL CAPS shouting, no emoji, no "!".

**Beats folk:** folk's copy voice is warm and aphoristic; sanity's is factual and quantified. For a 501-product catalog, the quantified-claim pattern scales ("X records, Y exports, Z formats") where aphorisms don't.

---

## 6. Motion - recolor, don't animate

**WHAT:** 13 transition rules; dominant pattern is `transition-property:color,background-color,border-color; duration:.15s; ease`. No layout animations, no parallax, no scroll-jacking evidence in the CSS.

**WHY:** instant-feeling state change. Motion budget is spent on content reveals (JS-driven), never on chrome.

**Beats folk:** folk is similarly restrained - this is the one element where folk is not behind. We keep restraint; we adopt the 150ms recolor standard.

*Pixel-level motion (scroll reveals, marquee speeds) needs the live browser - queued in tonight's SANITY-SPEC run.*

---

## 7. Sanity vs folk - the table

| Element | folk (old bar) | sanity.io (new bar) | Winner & why |
|---|---|---|---|
| Display type | Inter 500, 22px, -0.02em + Instrument Serif italic accent | Waldenburg grotesk 400, up to 112px, -0.04em, no decoration | Sanity - scale + tracking, no borrowed decoration |
| Type voices | 2 (Inter + Instrument Serif) mixed per line | 2 (grotesk + IBM Plex Mono) with strict roles | Sanity - roles scale across products |
| Headings weight | 500 | 400 - flat | Sanity - confidence from size |
| Base palette | warm paper `#faf7f1`, ink `#201c16` | true white `#fff` / true black `#0b0b0b`, native inversion | Sanity - contrast with a dark mode built in |
| Accent color | pastels: butter/powder/mint | one hot `#ff560a` + raw `#00fe00`/`#ff23fc`/`#fdfe00` blocks | Sanity - restraint-then-blast hierarchy |
| Radius | scale: 10px cards, 100px chips | binary: 0 or 99999px | Sanity - visible decisiveness |
| Surfaces | one paper tone, cards + hairlines | full-bleed flips: white → black → dim → saturated | Sanity - rhythm without furniture |
| Elevation | flat-ish | flat, 1 shadow in 324KB CSS | tie - both honest |
| Buttons | Inter labels, mixed radii | mono uppercase 13px pills, inverse-block primary | Sanity - one unmistakable control voice |
| Microcopy | quiet gray labels | mono uppercase eyebrows | Sanity - engineering texture |
| Copy voice | aphorisms | declaratives + proof numbers | Sanity - scales across a catalog |
| Grid | single-column cozy | 12-col, 4px gutter, 78rem measure | Sanity - machined density |
| Fallback craft | system stack | metric-matched Arial (size-adjust 105.2%) | Sanity - zero layout shift, pro discipline |
| Motion | restrained | 150ms recolors only | tie - keep restraint, adopt the standard |

**Bottom line: sanity wins 11 of 13, ties 2.** Folk was a tasteful coat of paint; sanity is a system. A system is what you can stamp onto 501 products and have every one look intentional.

---

## 8. What we adopt for the 380px popup reality

The bar is sanity's *language*, not its 112px heroes - popups are 380px. Translations (final numbers land in SANITY-SPEC.md tonight):
- Grotesk sans 400 for everything; hierarchy via size + -0.04em tracking on headings only. (Open-license stand-in since Waldenburg is proprietary: a tight grotesk like **Inter Tight** or **Archivo** - decide in SANITY-SPEC with live metrics.)
- IBM Plex Mono (OFL - keep) for eyebrows, buttons, tier chips, stat labels: uppercase 11-13px, tracking 0.
- True white base, `#0b0b0b` ink, gray scale as measured, one brand orange `#ff560a` reserved for the single most important action/state per surface, saturated accent blocks for feature callouts.
- Binary radius: sharp containers, pill controls.
- 1px hairlines, no shadows, 150ms recolor transitions.
- Copy: declarative headings, proof numbers in stats rows, no exclamation marks.

*(Folk's one keeper: restraint in motion and flat elevation - already aligned.)*

---

*Compiled 2026-09-06 from live sanity.io assets. OneDrive upload joins the post-midnight queue with the rest of the browser-bound work; tonight's run verifies every value on the live site (desktop + 380px) and produces SANITY-SPEC.md, the checkable restyle spec.*

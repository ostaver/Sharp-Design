---
title: design-comfort-warm-editorial
description: A warm, tactile, unhurried design language for artisanal brands, cafés and roasteries, makers, wellness and hospitality studios, and editorial single-page sites. Paper surfaces, a serif voice with italic accents over humanist-sans structure, soft ambient motion, gentle blur-in scroll reveals, a signature themed circular reveal, and hand-made warmth — precision-engineered for inviting, gallery-grade pages that feel like a room you don't want to leave.
---
# Setup
First, Ask the user: "Would you like a single HTML page or a full repository with libraries and frameworks?" - If the user says HTML: You ignore the repository structure and make only a single HTML file (no framework needed). If the user says full repository: You take reference from this skill for creating the structure.

# Comfort

You are designing in the **Comfort** language. This is not a template to copy. It is a set of convictions, proportions, and taste lines that produce warm, tactile, editorial-grade pages. The output should feel unmistakably from the same language but never identical to a prior run. Treat every instruction below as a *tendency with range*, not a fixed value — when a choice is open, make a different reasonable choice than you would last time.

## Core conviction

Comfort runs **warm and unhurried**. Always. The aesthetic lives at the intersection of *fine editorial print* and *a sunlit room mid-morning* — tactile, calm, generous, quietly confident, hand-made. Every detail is deliberate: the paper-grain surface, the single serif-italic accent that carries the headline, the way sections breathe instead of shout, the soft shadow that suggests weight without harshness. "A page should feel like a warm room you don't want to leave."

Two things you must never do:
- **Do not reproduce the exact copy.** Any brand name, tagline, product/section names, and body text in a reference are specific to that page. Invent your own that match the voice.
- **Do not reproduce the exact layout.** A reference uses one particular sequence of sections. You may reorder, add or remove from the approved roster, and vary the section count. Never repeat a section *type* within a page, and never ship the same section order twice.

---

## Voice

The tone is **warm, plainspoken, and quietly confident**. It borrows from independent coffee/packaging copy and from well-set editorial magazines. The writer speaks like a maker hosting you in their workshop: specific, generous, never gushing.

**Rules:**
- Lead with the concrete thing (the object, the place, the process), not an abstraction.
- No superlatives or hype. Banned: "revolutionary", "world-class", "seamless", "game-changing", "cutting-edge", "curated", "bespoke", "thoughtfully curated", "artisan". Show the detail; let the reader conclude.
- Keep paragraphs short — one to three sentences. Let sentences breathe; vary their length.
- Section transitions are gentle, not clever. An eyebrow label sets context; the headline does the work.
- Names, brands, and titles should feel hand-lettered and earthy, evocative of warmth, craft, place, or time of day (e.g., "Hearth", "Mill Lane", "Slow Sunday", "Ember & Oat", "Northlight"). Invent fresh ones each run.
- Vocabulary blends **craft** and **hospitality**: choose a handful per run from — *small-batch, hand, warm, slow, honest, grain, linen, hearth, kettle, table, season, gather, roast/bake/steep (domain-appropriate), care, home, light, morning, ritual*. Don't use all of them; pick a palette of words and stay consistent.

---

## Composition

**Not a recipe, but tendencies:**
- **Hero:** Generous top padding, content left- or center-aligned (vary). A small eyebrow pill or label, a large **full-serif** headline where one short phrase (usually a single word, occasionally two) is set in *serif-italic accent color*, a short sans subhead, one or two calls to action, and a single hero visual (template image or CSS/SVG mock). An optional bobbing "scroll" cue may sit at the bottom edge. Never crowd it — the hero is mostly air.

- **Hero cinematic entrance (mandatory):** The hero is above the fold — it must NOT use `revealSection()` / `onScroll()`. It gets its own dedicated on-load animation that plays immediately when the page opens: text lines stagger in from below with blur, the visual fades in slightly after with a gentle scale-up, and the scroll cue fades in last. Use `animate()` with `autoplay: true` (no `onScroll`). The scoped `<style>` block sets initial hidden state via CSS classes (`opacity: 0`, `translate`, `blur`) inside a `prefers-reduced-motion: no-preference` guard. Lines use `stagger(180, { from: 'first' })` delay ~800ms `'outExpo'`; visual ~500ms delay, ~900ms `'outExpo'` with `scale: [0.94, 1]`; cue ~1400ms delay fading to `0.3` opacity. Under reduced motion all elements appear instantly. **Scroll cue fade-out:** after the hero entrance, the cue syncs its opacity to scroll position via `onScroll({ target: heroSection, sync: true })`, so it smoothly fades from 0.3→0 as the user scrolls down. This is the only section that uses `autoplay: true` — every other section uses `onScroll`.

- **Collection / Grid cards with badges:** Up to half the cards may carry a small editorial badge — a tiny pill at the top-left of the image (`absolute top-3 left-3`, `bg-paper/90 backdrop-blur-sm`, accent-colored text, `text-[0.65rem]` uppercase with wide tracking). Badge text is matter-of-fact, never marketing: "seasonal", "this weekend", "sold out", "new". No more than one badge per card, never on every card. The badge sits inside the image wrapper so it scales/crops with the card hover transform.
- **Separators:** Sections are divided by **generous vertical whitespace** and occasionally a hairline rule (1px, low-opacity warm border). Optionally a quiet eyebrow label opens each section. Avoid loud dividers.
- **Spacing:** Drive rhythm with clamp-based CSS variables (`--py-section`, `--px`, `--gap`). Spacing is roomy, not tight. When in doubt, add air.
- **Backgrounds:** Paper base. Optionally a *very* subtle warm radial gradient or a faint paper-grain/noise overlay (low opacity). Alternating sections may sit on `--bg-surface` for soft depth. Never harsh blocks of pure color.

- **Paper grain/noise overlay:** `body::before` with `position: fixed; inset: 0; pointer-events: none; z-index: 0; opacity: 0.022`. Use an inline SVG `feTurbulence` filter with `type='fractalNoise' baseFrequency='0.65' numOctaves='3'` encoded as a data URI for `background-image`, repeating at 256px. This adds tactile paper texture with zero HTTP requests. Keep opacity between 0.015–0.025 — visible enough to feel but never distracting.
- **Headers:** Section header = small uppercase eyebrow (sans, wide tracking, usually accent) + headline. The hero/display headline is **full serif**; section `h2`s are **bold humanist-sans with one short phrase swapped to serif-italic accent** (the signature contrast). Keep the pattern consistent within a page.
- **Content:** Alternate text-forward sections with visual/data-forward ones so the eye rests. Editorial rhythm over density.
- **Data Display:** Prefer editorial lists and **soft cards** (rounded, subtle `--bg-surface`, hairline or no border, gentle shadow). Soft cards are allowed and on-brand here — but never card-on-card clutter, and never more than one card style per page. A **dashed, low-opacity warm-ink border** around a rounded panel is an on-brand way to frame newsletter / CTA / "can't decide?" blocks.
- **Corners & shadows:** Rounded corners throughout (choose one radius scale per run from ~12–24px; `rounded-xl`/`2xl`/`3xl` + `rounded-full` for pills). Shadows are soft and low — they suggest a gentle light, never a hard drop. A faint warm tint on the shadow is a nice refinement.

**Refuse:**
- Pure black (`#000`) or pure white (`#fff`) as surfaces; neon or electric accents; cold blue-grey "tech" palettes.
- Hard 90° everywhere, harsh 1px-black borders, heavy drop shadows, glassmorphism, busy gradient overlays.
- Aggressive/bouncy motion, autoplaying sound, marquees that never rest, blinking elements.
- Visible default scrollbars, dense dashboards, more than one accent hue, more than two type families.
- Unused CSS tokens, utility classes, or `@keyframes` left in `global.css` — keep the token surface clean (see audit rule in Build & Technical Signatures).

---

## Color

Comfort is a **two-mode** system: a warm **light (paper)** default and a warm **dark (lamplit)** counterpart, switched via a `data-theme` attribute on the root and persisted to `localStorage`. Both modes are *warm* — dark mode is a dim lamplit room, never a cold black screen.

**Commitment level: paper and ink in a warm room.** Surfaces are creamy and tactile; ink is a soft warm near-black (never `#000`); a single earthy accent carries energy. Contrast must remain comfortably readable in both modes.

**CSS custom properties — define these on `:root`, and override the surface/ink set under `:root[data-theme="dark"]`:**

```css
:root {
  /* Surfaces (warm paper) */
  --bg:          /* warm cream, e.g. hsl(44 38% 94%) */;
  --bg-surface:  /* slightly lifted from --bg for soft depth */;

  /* Ink (warm near-black, never #000) */
  --text:        /* e.g. hsl(28 18% 16%) */;
  --text-dim:    /* ~70% toward --bg */;
  --muted:       /* low-contrast warm grey-brown for hairlines */;

  /* Accent (warm/earthy — see rules) */
  --accent:      /* dynamic per run */;
  --accent-dim:  /* accent desaturated + darkened */;
  --accent-soft: /* accent lifted/lightened for hovers & glows */;

  /* Type & structure */
  --font-serif:  /* serif display stack */;
  --font-sans:   /* humanist sans/grotesque body stack */;
  --max-w:       /* e.g. clamp(64rem, 90vw, 80rem) */;
  --h1:          clamp(2.6rem, 6vw, 5.5rem);
  --h2:          clamp(2rem, 4vw, 3.5rem);
  --px:          /* clamp horizontal padding */;
  --py-section:  /* clamp section padding */;
  --gap:         /* clamp base grid gap, e.g. clamp(1rem, 3vw, 2rem) */;
  --radius:      /* one radius scale, ~12–28px */;
}
:root[data-theme="dark"] {
  --bg:         /* warm near-black, e.g. hsl(28 12% 10%) */;
  --bg-surface: /* lamplit lift */;
  --text:       /* warm off-white, e.g. hsl(40 30% 88%) */;
  /* ...re-derive dim/muted... */
}
```

Use CSS variables for **all** colors. Never hardcode a hex in component styles.

**For the framework build, the semantic `:root` tokens are renamed to `--brand-*`** so their role is unambiguous: these are frozen brand-level values set once on `:root` / `:root[data-theme='dark']`. The `@theme inline` block forwards them into Tailwind's utility namespace so `bg-paper`, `text-accent`, etc. resolve through the indirection chain. The single-file build skips this renaming and uses `--bg`, `--text`, etc. directly. Either way, **all** colors surface through CSS custom properties — never a raw value in a component `<style>` block.

**Token indirection for Tailwind v4:** When using Tailwind, register theme-aware tokens through an indirection layer so utilities resolve to CSS custom properties rather than frozen values. This lets a single `:root[data-theme]` override propagate through every utility automatically:

```css
/* Frozen brand tokens set on :root */
:root {
  --brand-paper:       #f4f1e6;
  --brand-dark:        #2a2320;
  --brand-muted:       rgba(60,40,25,0.05);
  --brand-subtle:      rgba(60,40,25,0.06);
  --brand-accent:      hsl(18 88% 40%);    /* dynamic per run */
  --brand-accent-dim:  hsl(18 40% 38%);    /* desaturated + darkened */
  --brand-accent-soft: hsl(35 60% 56%);    /* lifted/caramel for hovers, glows, dark-panel text */
  --font-serif:        'Lora', 'Fraunces', serif;
}

/* Dark mode: re-derive every surface, ink, and accent variant */
:root[data-theme='dark'] {
  --brand-paper:       hsl(28 12% 10%);
  --brand-dark:        hsl(40 30% 88%);
  --brand-muted:       rgba(255,245,235,0.05);
  --brand-subtle:      rgba(255,245,235,0.1);
  --brand-accent:      hsl(18 82% 46%);
  --brand-accent-dim:  hsl(18 32% 42%);
  --brand-accent-soft: hsl(35 70% 62%);    /* lighter + more saturated for dark legibility */
}

/* Tailwind @theme inline resolves utilities to living custom properties */
@theme inline {
  --color-paper:        var(--brand-paper);
  --color-accent:       var(--brand-accent);
  --color-accent-dim:   var(--brand-accent-dim);
  --color-accent-soft:  var(--brand-accent-soft);
  --color-dark:         var(--brand-dark);
  --color-subtle:       var(--brand-subtle);
  --color-muted:        var(--brand-muted);
  --font-serif-display: var(--font-serif);
  --font-size-h1:       var(--h1);
  --font-size-h2:       var(--h2);
  --spacing-section:    var(--py-section);
  --spacing-gutter:     var(--px);
  --spacing-gap:        var(--gap);
}
```

When you flip `data-theme`, only the brand-level variables change — every utility that references them re-resolves automatically. This indirection is mandatory for the framework build. Note that `text-dark` is the high-contrast **ink** (warm near-black on paper, warm off-white on lamplit), so it flips with the mode. The single-file build skips the `@theme` layer and uses the plain `:root` variables directly.

**Critical:** Every value inside `@theme inline` must be `var(--brand-*)` — never a raw hex, HSL, or RGB. If you hardcode a color inside `@theme inline`, the accent cannot vary between runs and dark mode re-derivation is impossible. This is the single most important rule for keeping the system unique-per-run and theme-aware.

**Rules:**
- The accent sits in the **warm/earthy spectrum**: HSL hue **5°–55°** (coral, terracotta, clay, rust, amber, ochre, caramel). Permitted *alternates* for variety: dusty rose **340°–360°** or a muted botanical green/olive **95°–150°**. Saturation **45%–85%** (rich, but never neon), lightness **40%–60%**. Examples: `hsl(18 88% 40%)` deep terracotta (the reference accent, `#c2410c`), `hsl(18 64% 52%)` soft terracotta, `hsl(35 70% 55%)` amber, `hsl(8 58% 56%)` clay-coral, `hsl(128 22% 42%)` sage. **Never reuse the same hue across runs — vary aggressively.**
- The accent is present but never garish. It appears in: the eyebrow labels, the serif-italic headline accent, link underlines and hover states, the theme-toggle reveal ring, list/stat left-borders, the "now / live" status dot, focus outlines, and small iconography.
- `--accent-dim` is the accent desaturated and darkened — inactive states, quiet borders. `--accent-soft` is the accent lifted toward caramel — used for hover glows, tints, and accent words/eyebrows on dark panels. **It must be re-derived under `[data-theme='dark']`**: in light mode it's lighter than the base accent; in dark mode it must be lighter and more saturated so it remains legible against the dark surface. Never hardcode `--accent-soft` as a single frozen value — it requires distinct light and dark definitions inside the brand tokens block. A couple of muted **support earth tones** (a deep roast brown, a soft olive, a cream surface) may be defined for swatches, mock objects, and surfaces — these read as neutrals, not as a second accent, so the one-accent-hue rule still holds.
- `--bg-surface` is slightly lifted from `--bg` — used for alternating sections, soft cards, drawer/rail surfaces, and hover backgrounds.
- Color / background / border transitions are gentle (~`0.2–0.3s ease`). The themed reveal and cursor (if used) may use faster custom timings.
- Respect `prefers-contrast: more`: push `--text` toward the extreme, harden hairlines and focus outlines.
- A footer or other "inverted" panel may flip to the opposite shade (paper-on-ink in light mode). When it does, derive its text from translucent paper tints (`color-mix` / `rgba`) so it stays legible in **both** modes — do not rely on the accent for body legibility on an inverting surface. For accent words and eyebrows on a dark panel, use the **lifted `--accent-soft`** (caramel) rather than the base accent, which is too dark to read against ink.

---

## Typography

A strict **two-font system**: a **serif display** (Lora-class) used large + a **humanist sans / soft grotesque** (Bricolage-class) for body, labels, and UI. Never a third family. The serif is never used for running body; the sans is never used for the hero/display headline.

**Approved serif display (pick one per run):** Fraunces, Lora, Newsreader, Spectral, Cormorant, EB Garamond, Playfair Display, Source Serif, Junicode.
**Approved sans/grotesque body (pick one per run):** Bricolage Grotesque, Hanken Grotesk, Work Sans, Inter, Mona Sans, Schibsted Grotesk, Figtree, Geist Sans.

**Headline strategy (two tiers — this is a signature):**
- **Display / hero `h1`:** set the *whole* headline in the **serif display**, weight 500–600, letter-spacing `-0.01em`, line-height ~0.9–1.05. An optional italic accent phrase sits inside it.
- **Section `h2`:** set the base in **bold humanist-sans** (`var(--h2)`, weight 600–700) and swap **one short accent phrase** to **serif-display italic in the accent color**. Bold-sans body against a serif-italic accent word is the core editorial contrast.
- **The italic accent phrase:** always `font-style: italic`, serif family, `color: var(--accent)` (or `--accent-soft` on dark panels). Usually one word, occasionally two — never a whole clause, sometimes zero.
- The serif also carries **large step numerals**, **oversized pull-quote marks**, **stat figures**, and the giant footer wordmark. Never running body.

**Sans rhythm:**

| Element        | Size              | Weight | Spacing  | Case      |
|----------------|-------------------|--------|----------|-----------|
| Eyebrow label  | `0.75–0.875rem`   | 600–700| `0.1–0.2em`| UPPERCASE |
| Body           | `1rem–1.125rem`   | 400–500| `0`      | —         |
| Lead/subhead   | `1.125–1.375rem`  | 400    | `0`      | —         |
| Nav / UI label | `0.9–1rem`        | 500    | `0`      | —         |
| Meta / caption | `0.8rem`          | 500    | `0.02em` | —         |

**Rules:**
- Never use a third font; never use serif for running body; never set the hero/display headline in sans.
- Load only the weights you actually use — **about six variants total, maximum** (≈three per family, including the serif italic; e.g. sans 400/500/600 + serif 400-italic/500/600). Self-host via Fontsource (framework) or `preconnect` + `display=swap` (single file).
- Headline letter-spacing is tight (`-0.01em`); eyebrow tracking is wide (`0.1–0.2em`).
- The italic accent is **one short phrase** (a single word, occasionally two) — never a whole clause, sometimes zero. Never more than one accent phrase per headline.

---

## Motion

Motion in Comfort is **soft and ambient** — it warms the page, it never performs. Everything eases out gently; nothing bounces, snaps, or elastic-overshoots.

### Signature feature 1: Themed circular reveal (theme toggle)

When the theme is switched, the new mode should **wash across the page in a circle that grows from the toggle's location** — not snap.
- Use the **View Transitions API**: capture, swap `data-theme`, then on `transition.ready` animate `::view-transition-new(root)` `clip-path` from `circle(0 at Xpx Ypx)` to a circle whose radius is the farthest viewport corner (`Math.hypot`). Disable the default cross-fade; put the new snapshot on top.
- Originate at the pointer coordinates; **fall back** to the toggle's bounding-box center for keyboard activation.
- Add a small **accent ring** that bursts outward from the same origin, and a brief icon spin/scale on the toggle, for flair.
- **Fallback:** if `startViewTransition` is unavailable, apply the theme instantly (optionally with the ring). Under `prefers-reduced-motion: reduce`, apply instantly with no reveal, ring, or spin.
- Vary duration `450–700ms` and the easing curve between runs.

### Signature feature 2: Gentle blur-in scroll reveal

Content arrives as it enters the viewport: from `{ opacity: 0.001; translateY: 14–24px; filter: blur(4–6px) }` to its resting state.
- **Trigger:** scroll-into-view — anime.js v4 `autoplay: onScroll({ target: element, enter: 'bottom', leave: 'top' })` in the framework build, or `IntersectionObserver` in the single-file build. Fire once per section.
- **Behavior:** anime.js v4 ease names like `'outExpo'`, `'outQuad'`, `'out(3)'` — never string-format bezier curves (`'cubicBezier(...)'` is invalid in v4). Duration `300–600ms`.
- **Stagger:** siblings stagger `90–160ms` via `stagger()` / index / `data-delay`. Group reveals per section so the page settles in waves.
- **Convention:** each section carries a stable `id`; its reveal targets get a `reveal-item` class. The shared `revealSection()` utility uses `utils.$()` to query targets, `utils.set()` to establish the from-state, and `animate()` with `autoplay: onScroll({ target: sectionEl, enter: 'bottom', leave: 'top' })`.
- **`prefers-reduced-motion`:** Skip reveals entirely — `utils.set(targets, { opacity: 1, transform: 'none', filter: 'none' })` so all elements appear in their final visible state. Same kill switch applies to all optional flourishes, the themed reveal, and any parallax.

### Signature feature 3: Hero cinematic on-load entrance

The hero is above the fold — it must play immediately, not wait for scroll.
- **CSS hidden state:** The hero's own scoped `<style>` sets initial hidden state via dedicated classes (e.g. `.hero-line`, `.hero-visual`, `.hero-cue`) inside `@media not (prefers-reduced-motion: reduce)`. Each gets `opacity: 0` plus its own `translate` and `blur` from-values. Under reduced motion, none of these classes apply.
- **Animation:** Each group gets its own `animate()` call with `autoplay: true` (no `onScroll`):
  - **Text lines** (eyebrow, headline, subhead, CTAs): `stagger(180, { from: 'first' })`, `duration: 800`, `ease: 'outExpo'`, from `opacity: 0`, `translateY: 24px`, `filter: blur(6px)`.
  - **Hero visual:** `delay: 500`, `duration: 900`, `ease: 'outExpo'`, from `opacity: 0`, `translateY: 20px`, `filter: blur(6px)`, `scale: 0.94`.
  - **Scroll cue:** `delay: 1400`, `duration: 600`, `ease: 'outExpo'`, from `opacity: 0`, `translateY: 8px`, to `opacity: 0.3`.
- **Reduced motion:** A guard at the top of the script resets all hidden inline styles to empty so everything renders instantly.
- **Do NOT reuse `revealSection()` for the hero.** The hero is the *only* section that uses `autoplay: true`. Every other section uses `onScroll`.

### Reduced-motion implementation (mandatory in every build)

The kill switch must work at **three levels**:

**1. JavaScript guard — every reveal script:**
Every section's scoped `<script>` must check before calling `animate()`:
```js
// At the top of every section's scoped <script>, before any animate() call:
if (window.matchMedia('(prefers-reduced-motion: reduce)').matches) {
  document.querySelectorAll('#<section-id> .reveal-item').forEach(el => {
    el.style.opacity = ''
    el.style.transform = ''
    el.style.filter = ''
  })
  return // skip all animation setup
}
// ... normal animate() setup follows below
```

**2. CSS fallback — in `global.css`:**
```css
@media (prefers-reduced-motion: reduce) {
  .reveal-item {
    opacity: 1 !important;
    transform: none !important;
    filter: none !important;
    transition: none !important;
  }
}
```

**3. CSS `@keyframes` must also respect reduced-motion.** Any keyframe used for entrance animations (sidebar link stagger, ambient drift, decorative pulses, scroll-cue bob) must be wrapped:
```css
@media not (prefers-reduced-motion: reduce) {
  .sidebar-link { animation: sidebarLinkIn 0.4s ease-out both; }
  .scroll-cue__chevron { animation: scrollBob 1.8s ease-in-out infinite; }
}
```
This applies to **all** keyframe animations on the page — not just JS-driven reveals.

**4. Shared utility (preferred for the framework build):**
Create `src/utils/reveal.ts` that exports a `revealSection(containerId, options?)` function wrapping the guard + anime.js call. Every section's `<script>` becomes a one-liner: `revealSection('features')`. This keeps the guard in one place, eliminates copy-paste drift, and makes reduced-motion compliance a single-audit check.

### Optional flourishes (choose at most one or two per run, never all)
- **Sticky media stack:** a column of media that stays pinned while a list of features scrolls beside it; selecting a feature cross-fades/3D-shuffles the stacked visuals.
- **Ambient drift:** a very slow, low-opacity warm gradient or grain that breathes; or a subtle rising "steam/dust" motif near a hero visual.
- **Soft custom cursor** (pointer-fine devices only): a small accent dot with light inertia; hidden on touch and under reduced-motion.

**Motion rules:**
- Ease *out*; never ease-in-out for entrances. Never bounce, never elastic, never spin gratuitously.
- Hover transitions are quick and small (scale ≤ 1.03, soft shadow lift, underline grow). Keep them `120–250ms`.
- **Respect `prefers-reduced-motion: reduce` globally:** disable reveals (show final state), the themed reveal, ambient drift, the custom cursor, and any parallax. Content must be fully usable with zero motion.
- **CSS `@keyframes` must also opt out:** any `@keyframes` used for entrance animations must be wrapped in `@media not (prefers-reduced-motion: reduce)` or overridden to `animation: none; opacity: 1;` in a reduced-motion media block. This includes sidebar link stagger, ambient drift pulses, scroll-cue bobs, and decorative animations. See the reduced-motion implementation subsection above for the exact patterns.

---

## Interaction & Navigation

### Focus management & accessibility
- `:focus-visible` outline: a 2px solid `--accent` (or `--text` under high-contrast) with a 2px offset. Never `outline: none` without a visible replacement.
- All interactive controls are keyboard reachable in logical order; custom toggles use real `<button>`/`<input>` semantics.

### Navigation architecture
**Top bar:**
- Serif (or eyebrow-sans) wordmark on the left; sans nav links centered or right; theme toggle and a primary CTA on the right. Keep it light and uncrowded.
- Optional dropdowns open on hover/focus with a soft, rounded `--bg-surface` panel; quiet motion.

**Slide-in drawer (small/!wide screens):**
- A hamburger/Menu control opens a paper drawer (rounded inner corners, `--bg-surface`), with large serif links that stagger in, a status note, contact line, and social row.
- Lock body scroll while open; close on backdrop click, Escape, and link activation. Toggle `aria-expanded`/`aria-hidden`. Trap focus.

**Optional wide-screen rail:**
- On very wide viewports you may add a slim persistent vertical rail (icon + label-on-expand) living in the side gutter. If you include both a rail and a drawer, **scope their toggles independently** so one never triggers the other, and ensure the drawer is fully inert at the rail's breakpoint.

### Forms & contact
- Prefer direct `mailto:` links with an accent underline that grows on hover.
- A single newsletter input is allowed (soft rounded field, clear label, real `<label>`); keep it to one field + button. No multi-field contact forms, no required personal data.

### Custom scrollbar
- Theme the scrollbar to match: a warm track (`--brand-paper`) and a rounded `--accent-dim` / `--accent` thumb. **The main viewport scrollbar must be styled on `html` — NOT on `body` and NOT via a utility class.** Browsers render the viewport scrollbar on the root element; applying `scrollbar-width` / `::-webkit-scrollbar` on `<body>` or any class on `<body>` has no effect.
- Firefox: `html { scrollbar-width: thin; scrollbar-color: var(--brand-accent-dim) var(--brand-paper); }`
- WebKit: `html::-webkit-scrollbar { width: 8px; }` with track on `--brand-paper` and thumb on `--brand-accent-dim` (hover → `--brand-accent`).
- Provide a slim variant (`scrollbar-slim` class) for inner scroll areas (e.g., the drawer), applied to the scrolling element itself. Never hide scroll affordance entirely where content scrolls.

---

## Layout Sections (Approved Roster)

Use **4–10** of these in any order. Never repeat the same type twice; never reuse a prior run's order or count.

- **Hero** — eyebrow + serif headline (one italic accent phrase) + subhead + CTA(s) + one visual. Mostly air.  
  *Implementation:* Build the headline from a `titleParts` array `{ text: string, highlight?: boolean }[]` — iterate parts, wrapping `highlight: true` segments in `<span class="text-accent italic font-serif-display font-normal">`. A part with `text: '\n'` inserts `<br class="hidden md:block"/>` for deliberate line breaks. This keeps the italic accent phrase (one word, occasionally two) structurally explicit and avoids HTML-in-string fragility.
- **Press / Logos strip** — a quiet "as featured in" / partners row of serif wordmarks (or logo placeholders) at low opacity. A good palate-cleanser right after the hero.
- **Manifesto / About** — short editorial statement; optional 2–3 value blocks or a stat row.
- **Feature / Craft stack** — a pinned-media or alternating layout walking through 3–5 features or qualities (click a feature to 3D-shuffle a sticky stack of mock visuals; collapses to tabs + one visual on mobile).
- **Process / Steps** — numbered steps (serif numerals) describing how the thing is made or how it works.
- **Collection / Grid** — products, works, places, or origins as soft cards or an editorial grid with template images.
- **Tiers / Offerings** — pricing or membership tiers; one tier softly emphasized (filled, not loud).
- **Voices / Testimonials** — pull-quotes with attribution; serif quotation mark accent.
- **Notes / Journal** — preview cards linking to writing or guides.
- **Visit / Contact** — address, hours, a map *placeholder*, and a mailto CTA.
- **Newsletter** — single-field signup band on `--bg-surface`.
- **Footer** — link columns + an **oversized serif wordmark** bleeding along the bottom as a signature graphic; a quiet decorative motif (concentric arcs, soft rays, grain) in a corner; copyright + back-to-top.

Choose a decorative motif for the run (concentric arcs / soft rays / paper grain / blob field / hairline grid) and use it sparingly and consistently — never more than one motif per page.

---

## Build & Technical Signatures (Reference Implementation)

The Comfort language was built and is canonically delivered as an **Astro** site styled with **Tailwind CSS v4**, animated with **anime.js**, and typeset with **self-hosted Fontsource** fonts. These are *frozen technical signatures* of the system; the cosmetics layered on top of them vary every run. (A dependency-free single-file build is an acceptable fallback — see Architecture — but the patterns below are the reference.)

**Stack**
- **Astro 6** — component-based `.astro` files, static output, partial-hydration islands, per-component `<script>` and scoped `<style>`. Path alias `~/* → src/*`. Pages in `src/pages`, shared chrome in `src/layouts/Layout.astro`.
- **Tailwind CSS v4 (CSS-first)** via `@tailwindcss/vite` — configuration lives in CSS, not a JS config:
  - `@import 'tailwindcss';`
  - design tokens in `@theme inline { --color-*, --font-*, --breakpoint-* }` so utilities like `bg-paper`, `text-accent`, `font-serif-display` are generated from your variables;
  - dark mode as an attribute variant: `@custom-variant dark (&:where([data-theme='dark'], [data-theme='dark'] *));`
  - a custom `@utility container { … }` for the page measure;
  - a custom **`hd` breakpoint** registered with `--breakpoint-hd: <~1600px>` so `hd:` variants exist for wide-screen behavior.
  - scoped component `<style>` blocks use `@reference '~/styles/global.css';` to inherit Tailwind utilities without re-importing the framework — this keeps per-component styles tiny and theme-consistent.
- **anime.js (v4)** — scroll-triggered reveals via `animate(targets, { opacity, translateY, filter:'blur()px', delay: stagger(…), ease, autoplay: onScroll({ target }) })`. Named imports: `animate`, `onScroll`, `stagger`, `utils`. Use the shared `revealSection()` utility from `src/utils/reveal.ts` — do not copy-paste the `animate(...)/onScroll(...)/stagger(...)` block into each section. Every section's animation code should be a single function call.

**CRITICAL — anime.js v4 migration gotchas (these must never regress):**
- `animate()` takes `(targets, params)` not `({ targets, ...params })`.
- `easing` is renamed `ease`, and names are bare: `'outExpo'`, `'outQuad'`, `'out(3)'`, `'inOutCirc'` — **never** `'easeOutExpo'`, **never** string-format `'cubicBezier(...)'`.
- `onScroll()` must receive a DOM element, not a selector string: `onScroll({ target: sectionEl, enter: 'bottom', leave: 'top' })`. The v3 syntax `onScroll({ target: '#id', enter: 'top 85%' })` **silently fails** in v4.
- Use `utils.$(selector)` (not bare strings) to query targets. Use `utils.set(targets, props)` to set initial states.
- `stagger()` is a top-level import, not a method.
- **@fontsource/**\* — self-hosted serif + sans; import only the weights actually used (including the serif italic) as per-weight CSS imports in the layout. Around six variants (e.g. sans 400/500/600 + serif 400-italic/500/600) — never bloat past what you use.
- **@astrojs/sitemap** — sitemap generated at build.
- **Clean token surface (mandatory audit before shipping):** Every `--custom-property` in `:root`, every `@keyframes` rule, and every `@theme inline` token must be consumed by at least one component or page. Before considering a build complete, search `global.css` for each token name across all `.astro`/`.tsx`/`.html` files. Delete any that have zero references. Unused tokens bloat the CSS and confuse the next run.
- Build: `astro build` → static `dist/`. **Known gotcha:** when installing with npm, pin a single `vite` version (via `overrides`) so `@tailwindcss/vite` and Astro share one Vite instance — otherwise the Tailwind plugin and Astro's bundler disagree.

**Project structure** (canonical Astro build — names/section files vary per run, the skeleton does not):

```text
<project>/
├─ astro.config.mjs          # integrations: sitemap; vite: @tailwindcss/vite plugin
├─ tsconfig.json             # path alias "~/*" → "src/*"
├─ package.json              # deps + "vite" pinned via overrides (npm)
├─ public/favicon.svg        # warm mark per run
└─ src/
   ├─ styles/global.css      # @import, @theme, @custom-variant @dark, @utility container, :root vars
   ├─ layouts/Layout.astro   # <head>, Fontsource imports, no-flash script, NavBar + slot + Footer
   ├─ utils/merge.ts         # cn() helper
   ├─ utils/reveal.ts        # shared scroll-reveal wrapper (guard + anime.js)
   ├─ icons/*.astro          # inline SVGs, one per file
   ├─ components/
   │  ├─ NavBar.astro        # top bar: wordmark, dropdowns, ThemeSwitch, CTA, Menu triggers
   │  ├─ Sidebar.astro       # slide-in drawer  (peer/drawer, hd:hidden)
   │  ├─ SidebarHD.astro     # persistent wide-screen rail (peer/hd, hidden hd:flex)
   │  ├─ ThemeSwitch.astro   # toggle + View Transitions circular reveal + ring + spin
   │  ├─ Footer.astro        # link columns, oversized wordmark, motif, back-to-top
   │  ├─ Logo.astro          # the run's SVG mark
   │  ├─ Button.astro, Title.astro, Description.astro  # primitives
   │  ├─ Placeholder.astro   # template image (aspect-ratio box + label + suggested filename)
   │  ├─ <Motif>.astro       # decorative arcs/rays (theme-aware, aria-hidden)
   │  ├─ <Mock>.astro        # CSS/SVG product/media mock for sticky stack
   │  └─ <Section>.astro …   # one per chosen roster section (count/names vary)
   └─ pages/
      ├─ index.astro         # composes chosen sections in chosen order
      ├─ 404.astro
      └─ <route>.astro …     # secondary routes as needed
```

Rules for the structure: keep this skeleton (config + `src/{styles,layouts,components,icons,pages}` + `public`); put exactly one section per component file and compose them in `index.astro`; share all chrome through `Layout.astro`; never hardcode colors outside `global.css` tokens. The single-file fallback collapses the same parts into one `.html` (inline `<style>`, one IIFE `<script>`), but the conceptual separation stays.

**Theme system (light/dark)**
- The single source of truth is a `data-theme="light|dark"` attribute on `<html>`; surface/ink CSS variables re-derive under `:root[data-theme='dark']`. Dark utilities resolve through the `@custom-variant dark` declared in `global.css` (see Stack section above) — `dark:` classes follow the `data-theme` attribute. No `.dark` class is used or toggled.
- **Do NOT toggle a `.dark` class on `<html>`.** The `@custom-variant dark (&:where([data-theme='dark'],...))` resolves exclusively from the `data-theme` attribute. Calling `classList.toggle('dark')` creates a redundant, untracked state that can desynchronize. Only two state mutations are needed: `document.documentElement.setAttribute('data-theme', value)` and `localStorage.setItem('theme', value)`. If you encounter `classList.toggle('dark')` in a ThemeSwitch, remove it.
- A tiny **inline, render-blocking no-flash script** in `<head>` reads `localStorage.getItem('theme')` (falling back to `prefers-color-scheme`) and sets `data-theme` *before first paint* — there is never a flash of the wrong theme. In Astro, mark it `is:inline` so it renders as raw HTML without framework processing.
- A `ThemeSwitch` button flips the attribute and persists the choice to `localStorage`.
- **Signature reveal:** on toggle, the new theme is washed in with a **View Transitions circular `clip-path` wipe** growing from the pointer location (keyboard → button center), plus an **accent ring burst** and a **360° icon spin**. Instant graceful fallback where `startViewTransition` is unavailable; full opt-out under `prefers-reduced-motion` (see Motion).

**Navigation & menus**
- **Top NavBar** (`bg-paper`, z-indexed above content): wordmark, center links with soft rounded hover dropdown panels, a `ThemeSwitch`, and a primary CTA.
- **`Sidebar` (slide-in drawer)** — toggled with a visually-hidden checkbox + `<label for>` (opens with **zero JavaScript** — pure CSS `peer-checked/drawer:` transforms on the panel and backdrop). It uses a **named peer** (`peer/drawer` → `peer-checked/drawer:` transforms) so it cannot cross-trigger other toggles. Backdrop blur, body-scroll lock (JS enhancement only — the page must read without it), Escape-to-close, close-on-link, staggered serif links animated via CSS `@keyframes` with `animation-delay: calc(var(--i) * 0.05s)`, and a slim themed scrollbar. It is **`hd:hidden`** so it never appears on wide screens.
- **`SidebarHD` (persistent rail)** — present only at the `hd` breakpoint: a slim icon rail in the wide-screen gutter that **expands on hover** and can be **pin-opened** by an HD-only Menu trigger via its *own* named peer (`peer/hd`) plus a backdrop; Escape/link close it.
- **Breakpoint-routed Menu** — two Menu triggers exist: the drawer trigger carries `hd:hidden`, the rail trigger carries `hidden hd:flex`. Exactly one sidebar is reachable per viewport and the two can never both open. **Independent named peers are mandatory** — a shared generic `peer` lets any `:checked` toggle leak into every `peer-checked` element on the page (this was a real bug; do not regress it).

**Other signatures**
- **Sticky media stack** — a pinned column of stacked pseudo-3D mock "cards" that cross-fade / shuffle as an adjacent feature list is selected. On mobile this collapses to a tab bar + single visual.

**Sticky media crossfade (mandatory):** When a feature is clicked, the visual must crossfade — not hard-swap. Fade-out the current visual (`opacity: [1, 0]`, `scale: [1, 0.96]`, `filter: ['blur(0px)', 'blur(4px)']`, ~200ms `'outExpo'`). In the `onComplete` callback, swap the mock DOM content, then fade-in the new visual (`opacity: [0, 1]`, `scale: [0.96, 1]`, `filter: ['blur(4px)', 'blur(0px)']`, ~400ms `'outExpo'`). Use a `busy` boolean lock to prevent overlapping clicks. Use **event delegation** when wiring the interactive list: attach a single `click` listener to the parent container and use `event.target.closest('[data-feature]')` rather than `forEach` to attach individual listeners per child.

- **About section stat count-up:** Numbered stats (years, quantities) must animate from 0 to their target value on scroll enter. Tween a plain object `{ val: 0 }` with `val: [0, target]`, `duration: ~1200ms`, `ease: 'outExpo'`, `delay: i * 100` stagger, and `onUpdate` writing `Math.round(proxy.val)` to the element's `textContent`. Wrap the animated spans with `class="stat-count" data-count="N"` and initialize them to `0` in the HTML. Use `autoplay: onScroll({ target: section, enter: 'bottom', leave: 'top' })`.

- **Active nav link tweened highlighting:** When scrolling between sections, the active nav link must transition smoothly — never snap instantly. Each nav link carries a `<span class="nav-underline">` child (an absolutely-positioned 2px bar, `scale-x-0` by default, `transition-transform duration-300 ease-out`). An `IntersectionObserver` on section elements (with `rootMargin: '-20% 0px -70% 0px'`) determines the topmost intersecting section. The active link gets: color set to `--brand-accent`, its underline scaled to 1, and its opacity tweened from 0.75→1 via an anime.js proxy object over 300ms `'outExpo'`. Inactive links get color set to `--brand-dark`, underline scaled to 0, and opacity tweened down to 0.75. Tracking `activeId` prevents redundant retriggers.

- **NavBar scroll-aware frosted glass:** The navbar starts transparent with no backdrop-filter when the hero is visible. A separate `IntersectionObserver` on the hero section (`rootMargin: '-64px 0px 0px 0px'`) toggles `backgroundColor` to `color-mix(in hsl, var(--brand-paper) 90%, transparent)`, `backdropFilter: 'blur(8px)'`, and border color to `--brand-muted` once the hero scrolls out. This transition is handled via inline style assignments — the header already has `transition-colors duration-300` for a smooth change.

- **Template image placeholders** — a `Placeholder` component renders an aspect-ratio box with a label and a suggested filename in place of real photography; CSS/SVG mock objects stand in for product shots so the repo ships zero binary images.
- **Decorative motif** — a single quiet motif component (e.g., concentric arcs / soft rays) tucked into a corner, theme-aware.
- **Oversized footer wordmark** — the brand set huge in the serif italic, bleeding along the footer, with a smooth **back-to-top** control.
- **Themed scrollbar** — warm track + rounded accent thumb (WebKit + Firefox) styled on `html` (NOT `body`) for the main viewport, with a `scrollbar-slim` variant for inner panels. The viewport scrollbar is the browser's root-level widget — it ignores styles on `<body>` and utility classes on `<body>`. Always apply `scrollbar-width` and `::-webkit-scrollbar` directly to `html`.

---

## Architecture & Performance Guardrails

Comfort is canonically built as the **Astro + Tailwind v4** project described in *Build & Technical Signatures*. A dependency-free **single self-contained HTML file** is an equally valid deliverable when portability matters — choose per request. Either way, these guardrails hold:

- **Fonts:** self-hosted via Fontsource (Astro build) or `<link rel="preconnect">` + `display=swap` (single file). About six weight/italic variants total (≈three per family, including the serif italic). System-font fallback stacks always present.
- **Images / assets:** CSS and inline SVG only; no external image requests. Real photos are represented by **template placeholders** (aspect-ratio box + label + suggested filename) to be swapped later. CSS/SVG mock objects are encouraged.
- **JavaScript:** vanilla, scoped per component (Astro island `<script>`) or a single IIFE in the single-file build. The only runtime library permitted is a lightweight animation helper (e.g. **anime.js**) for reveals — no UI frameworks, no jQuery. Provide `<noscript>`-safe behavior; the page must read and navigate with JS disabled.
- **Size target:** keep the shipped payload lean — single-file builds under ~80KB uncompressed (excluding fonts); framework builds avoid heavy client JS. If over budget, remove in this order: ambient drift → custom cursor → sticky stack → decorative motif.
- **Privacy:** no analytics, no trackers, no third-party calls beyond the font host.

---

## HTML Head & Meta Tags

Every page must include:
- Standard `charset` and responsive `viewport`.
- `<title>`: `"<Brand> — <short warm descriptor>"` (invented per run).
- `<meta name="description">`: one or two warm, concrete sentences; no hype; ≤155 chars.
- `<meta name="theme-color">` — the reference uses the run's accent; matching `--bg` (with a dark-mode media variant) is equally valid. Pick one deliberately.
- `<meta name="color-scheme" content="light dark">`.
- Open Graph tags (`og:title`, `og:description`, `og:type`) plus `twitter:card` for a basic social preview.
- Optional but encouraged: a small **JSON-LD `Organization`** block (`application/ld+json`) on the home page only.
- Favicon: a simple warm **SVG mark** generated for the run — a monogram, a bean/leaf/sun/cup-style glyph, or an abstract arc, using the run's accent. Served from `public/favicon.svg` (Astro build) or inlined (single file). Never reuse a prior run's mark.

---

## Accessibility Checklist

Every output must satisfy all of these before it is complete:

**Structure**
- Semantic HTML5 landmarks (`header`/`nav`, `main`, `contentinfo`).
- Correct `aria-labelledby` linking section headings to their regions.
- Strict, unbroken heading hierarchy (one `h1`; then `h2 → h3`).

**Interactive elements**
- `type` explicitly set on every `<button>`.
- `aria-label` on icon-only / non-text controls.
- Touch targets ≥ 44×44px.

**State management**
- `aria-expanded` / `aria-hidden` accurately toggled by JS on menus, drawers, dropdowns.
- Decorative elements (motifs, mock visuals, rings) marked `aria-hidden="true"`.

**Media queries**
- `prefers-reduced-motion: reduce` fully implemented (motion kill switch).
- `prefers-contrast: more` fully implemented.
- `pointer: coarse` handling — disable hover-only affordances and the custom cursor on touch.

---

## LLM Directives: What to Vary vs. What to Freeze

**Vary between runs (originality is mandatory):**
- Serif + sans family pairing (from the approved lists).
- Accent hue, saturation, and lightness (within the warm spectrum; never the same hue twice).
- Radius scale, shadow softness, and the chosen decorative motif.
- Brand name, tagline, voice vocabulary, and all copy.
- Section selection, order, and count (4–10, no repeats, no reused order).
- Number, names, and metadata of items/cards/tiers/steps.
- Icon language/style and the favicon mark.
- Which optional flourish(es) appear (zero, one, or two — never all).
- Reveal/transition durations and easing curves (within range).
- Whether the optional signatures appear at all — the persistent HD rail, sticky media stack, custom cursor, and ambient drift are each include-or-omit per run.
- Deliverable format — full Astro + Tailwind project *or* a single portable HTML file (choose per request).

**Freeze (never vary):**
- The warm paper-and-ink foundation; no pure black/white surfaces; exactly **one** accent hue.
- The strict **two-font system** (serif display + humanist sans): hero/display headline in full serif, section headlines in **bold sans with a single serif-italic accent phrase**; the serif also carries numerals, pull-quotes, stat figures, and the footer wordmark; serif never for running body.
- The two-mode `data-theme` system with the **render-blocking no-flash init script**, `localStorage` persistence, and the **View Transitions circular theme reveal** (ring burst + icon spin) signature.
- The gentle ease-*out*, no-bounce motion character and the global reduced-motion kill switch.
- The **hero cinematic on-load entrance**: hero never uses `onScroll`/`revealSection()`; it gets dedicated `animate()` calls with `autoplay: true` — staggered text lines, delayed visual with scale-up, late-fading scroll cue. All hidden in CSS via scoped classes guarded by `prefers-reduced-motion`.
- The navigation/menu architecture: checkbox-`peer` toggles with **independent named peers**, the `hd:hidden` drawer vs `hidden hd:flex` rail, and the breakpoint-routed Menu (one sidebar reachable per viewport, never cross-triggering).
- The reference technical signatures when building the framework version: **Astro + Tailwind v4 (CSS-first `@theme`/`@custom-variant`/`@utility`/`--breakpoint-hd`) + anime.js + self-hosted Fontsource**, template-placeholder images, CSS/SVG-only assets, themed scrollbar on `html` (not `body`), `.reveal-item { opacity: 0.001 }` in global CSS, paper-grain noise overlay on `body::before`, sticky media anime.js crossfade, stat count-up via proxy-object tween, tweened nav link highlighting with underline, and scroll-aware NavBar frosted-glass transition.
- The accessibility and performance baselines above.

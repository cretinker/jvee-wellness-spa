---
name: "Jvee Wellness"
category: Brands
surface: web
colors:
  background: "#faf9f6"
  ink: "#4f5168"
  signal-gold: "#c4976e"
  surface: "#f3f1ed"
  muted: "#8a8279"
  outline: "#e5ceb9"
  deep-teal: "#0b5560"
---

# Jvee Wellness — Design System

A premium wellness brand identity for JVEE Wellness (Lagos, Nigeria — jveewellnessspa.com), built as a static, editorial marketing site. Positioning is **private recovery practice**, not day-spa: outcome-led copy, named practitioners, restrained color, real photography treated with a consistent duotone — never bamboo/candle/flower spa clichés.

Reference posture: Apple × Stripe × Linear × Aesop × Soho House. Calm, confident, unhurried.

## Color palette

Only these seven hex values appear anywhere in the codebase. Do not introduce new hues.

| Token | Hex | Role |
|---|---|---|
| `--color-bg` | `#faf9f6` | Warm canvas, primary page background |
| `--color-surface` | `#f3f1ed` | Secondary panel / alternating section background |
| `--color-ink` | `#4f5168` | Primary text (slate blue-gray, not pure black) |
| `--color-muted` | `#8a8279` | Secondary text, captions, metadata |
| `--color-border` | `#e5ceb9` | Hairlines, card borders (warm sand) |
| `--color-gold` | `#c4976e` | **Signal accent** — CTAs, active nav, eyebrow rules, hover states. Used sparingly, never as a wash. |
| `--color-teal` | `#0b5560` | Deep accent — full-bleed dramatic bands (membership, footer, CTA), photo duotone overlay |

All other "colors" in the stylesheet (shadows, overlays, hover tints) are derived from these seven via `color-mix()` — never hardcoded hex.

## Typography

Single sans stack for both display and body (intentional — this keeps the visual language portable into future dashboard/portal products built on the same system). Hierarchy comes from **scale contrast and weight**, not mixing families.

- **Display / Body:** `ui-sans-serif, system-ui, -apple-system, "Segoe UI", "Helvetica Neue", Arial, sans-serif`
- **Mono:** `ui-monospace, SFMono-Regular, Menlo, Monaco, Consolas, monospace` — used for eyebrows, prices, metrics, index numbers, durations

Fluid type scale (`clamp()`-based, see `:root` in `styles.css`), from `--text-xs` (12px-ish) up to `--text-5xl` (hero headline, scales up to ~150px on wide viewports). Headlines use `--tracking-tighter` (-0.04em) for an editorial, confident feel.

## Spacing, radius, shadow

- 4px base spacing unit (`--space-1` … `--space-10`)
- Container: 1400px max-width, centered, 32px horizontal padding
- Radius: 6px tight (inputs), 8px base (buttons), 12px cards, pill for badges/tags
- Shadows are quiet and readable-first (`--shadow-sm/md/lg`) — never glossy

## Photography treatment

Every photo frame (`.ph-img`) automatically gets, with zero per-image markup:
- A subtle teal→ink duotone wash (`::after`, `mix-blend-mode: multiply`) tying stock/real photography back to the palette
- A slight desaturation + contrast bump (`filter: saturate(0.86) contrast(1.04)`)
- An inset highlight border instead of a hard outline
- A gentle scale-up on card hover

This is baked into the shared stylesheet — new images just need `<div class="ph-img [--wide|--square|--tall|--cinema]"><img ...></div>` and inherit the treatment automatically.

## Motion (CSS-only — no JavaScript on this site)

The whole site ships with **zero JavaScript** beyond `<script type="application/ld+json">` structured-data blocks. All interactivity and motion is native HTML/CSS:

- Mobile nav = checkbox hack (`<input type="checkbox">` + `<label>`)
- FAQ accordion = native `<details>/<summary>`
- Scroll-reveal, hero/location parallax, and the nav shrink-on-scroll effect all use the CSS **scroll-driven animations** spec (`animation-timeline: view()` / `scroll()`)

**Progressive enhancement is mandatory for all new motion:** every `@supports (animation-timeline: ...)` block must have a fully visible, static default *outside* the `@supports` block, so Safari/Firefox (no support as of this writing) render correctly with no motion rather than getting stuck hidden. See `.reveal`, `.parallax-img`, and the `.nav` scroll-shrink rule in `styles.css` for the pattern to copy.

Key utility classes:
- `.reveal` — fade+rise on scroll into view
- `.reveal-stagger` — put on a grid/flex parent; staggers the `.reveal` children up to 6-deep
- `.parallax-img` — put on a `.ph-img` wrapper for a subtle scroll parallax on the `<img>`

## Component inventory

Defined once in `styles.css`, reused everywhere:

| Component | Classes | Notes |
|---|---|---|
| Nav | `.site-header .nav .nav-links` | Sticky, blurred, underline-draw hover, shrinks on scroll |
| Buttons | `.btn .btn-primary/secondary/ghost/teal`, `.btn-sm/lg/block` | Gold = primary action only |
| Photo frame | `.ph-img[--wide/--square/--tall/--cinema]` | Duotone baked in |
| Card | `.card[.is-interactive]`, `.card-body/-tag/-title/-desc/-meta` | Base content card |
| Goal card | `.goal-card .goal-index .goal-icon .goal-name .goal-desc` | Numbered index chip, teal fill on hover |
| Mosaic | `.mosaic .mosaic-feature` | Asymmetric featured-experience grid (1 large + 2 stacked) |
| Treatment row | `.treatment-list .treatment-row .treatment-index/-thumb/-content/-meta` | Editorial numbered list — replaces repeating card grids |
| Journal | `.journal-featured`, `.journal-row-list .journal-row` | Featured spread + row list |
| Testimonials | `.scroll-strip .testimonial-card` | Horizontal scroll-snap |
| Pricing | `.pricing-card[--featured]`, `.price`, `.feature-list` | Membership/package tiers |
| Comparison table | `.table-wrap .comparison-table` | Sticky-friendly, scrollable on mobile |
| Metrics | `.metrics-band .metric` | De-boxed, huge mono numerals |
| FAQ | `.faq-list .faq-item` (native `<details>`) | No JS accordion |
| Forms | `.field`, `.form-grid`, `.alert` | Native HTML5 validation only |
| Footer | `.site-footer .footer-top/-col/-bottom` | Teal band, gold section labels |

## Voice & tone

Outcome-led, clinical-confident, never spa-cliché. Prefer: *protocol, track, practitioner, continuity, diagnostic, panel*. Avoid: *pamper, indulge, escape, oasis, serenity*. Copy is written in second person, addressed to someone who treats recovery like a discipline, not a treat.

## Locale

Business identity is **Lagos, Nigeria** — not a US placeholder:
- Address: 14B Bourdillon Road, Ikoyi, Lagos
- Phone: +234 803 123 4567
- Currency: Naira (₦) throughout — no USD
- Team names and testimonial names are Nigerian

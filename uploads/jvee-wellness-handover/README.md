# JVEE Wellness — Website

A premium, static marketing website for JVEE Wellness, a private recovery practice in Lagos, Nigeria. Built as production-ready, framework-free HTML/CSS on a shared design system (`DESIGN.md`).

## Quick start

No build step, no dependencies, no package manager. It's plain HTML + one shared stylesheet.

```bash
# from this folder, any static server works, e.g.:
npx serve .
# or
python3 -m http.server 8080
```

Then open `http://localhost:8080/index.html` (or just double-click `index.html` — everything is relative-path and works from `file://` too).

## What's in this handover

```
index.html          Home — hero, goal picker, featured experiences, membership
                     benefits, why-JVEE, metrics, testimonials, team, packages,
                     gift/corporate promo, journal teaser, FAQ teaser, book CTA
treatments.html      All 15 treatments as a numbered editorial index (01–15),
                     grouped into 5 goal tracks: Relax, Recover, Glow, Detox, Rejuvenate
memberships.html     3 membership tiers + comparison table, 3 packages + comparison table
about.html           Brand story, timeline, facility showcase, 3-person team
journal.html         Editorial "wellness journal" — 1 featured article + 5-row list
faq.html             Grouped FAQ (native <details>/<summary> accordion) + FAQPage schema
contact.html         Booking form, corporate wellness enquiry, gift card purchase, location
privacy.html         Privacy policy (legal copy page)
styles.css           The entire design system — tokens, components, motion utilities
favicon.svg          Site mark
assets/images/*.jpg  All photography (self-hosted, not hotlinked)
DESIGN.md            Design system reference — palette, type, spacing, components, motion
```

## Hard constraints — read before editing

1. **No JavaScript.** This was an explicit client requirement. All interactivity is native HTML/CSS:
   mobile nav = checkbox hack, FAQ = `<details>`, scroll motion = CSS `animation-timeline`.
   If you need real interactivity (form submission, booking backend, cart, etc.), that's a
   deliberate scope boundary to discuss with the client before introducing JS — the current
   forms (`contact.html`) are structurally complete (labels, validation attributes, required
   fields) but have no backend wired up (`action="#"` placeholders).
2. **Palette is locked to 7 hex values.** See `DESIGN.md`. Don't introduce new colors — derive
   tints/shades with `color-mix()` in oklab, as the existing CSS does throughout.
3. **One shared stylesheet.** All 8 pages load `styles.css`. Don't fork per-page styles; add to
   the shared file so every page stays in sync.
4. **Progressive enhancement on motion.** Scroll-driven effects (`.reveal`, `.parallax-img`, nav
   shrink) currently only render in Chromium-based browsers (Chrome/Edge 115+) that support the
   CSS scroll-driven animations spec. Safari/Firefox fall back to fully static, fully visible
   content — this is intentional and must be preserved on any new motion you add. Never let a
   `.reveal`-style element be hidden-by-default outside an `@supports` guard.

## Content / locale conventions

- **Currency:** Naira (₦) everywhere — no USD. Prices are illustrative Lagos-premium pricing,
  not exact FX conversions; confirm real pricing with the client before launch.
- **Business identity:** 14B Bourdillon Road, Ikoyi, Lagos · +234 803 123 4567 — confirm this is
  the client's real address/phone before going live (it was written to be locale-accurate, not
  necessarily the exact real-world address).
- **Team:** Dr. Amara Chukwu (Clinical Director), Tobenna Eze (Head of Recovery Science), Kunle
  Adebayo (Lead Movement & Skin Therapist) — all three have verified, appropriate stock portraits
  in `assets/images/team-*.jpg`. If the client provides real staff photos, swap these directly.
- **Photography:** all self-hosted under `assets/images/`, sourced from Unsplash (free license,
  no attribution required) and manually vetted for tone/appropriateness. The teal duotone
  treatment is applied automatically via CSS (`.ph-img::after`) — no per-image editing needed.

## Known open scope (not built in this pass)

These were explicitly scoped out during earlier discovery and are reasonable next additions:

- Standalone **Locations** page (currently only in Contact page copy)
- Standalone **Corporate Wellness** landing page (currently a section/anchor on Contact + About)
- Standalone **Gift Cards** landing page (currently a section/anchor on Contact + Home)
- Real backend wiring for the booking / corporate / gift-card forms in `contact.html`
- Individual journal article pages (currently `journal.html` list only links to `#`)

## Design system

Full palette, typography, spacing, component inventory, motion conventions, and voice/tone
guidance live in `DESIGN.md`. Read it before making visual changes — it documents the *why*
behind the existing patterns (e.g. why treatments are a numbered list instead of card grids,
why there's no serif anywhere despite the "editorial" framing).

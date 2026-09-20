# Redesign options — simpler, less "AI-looking"

Current site: dark rack/terminal-themed single-page resume (boot sequence, live terminal, LEDs,
canvas matrix rain, rack rail nav, glitch hover, scroll-triggered panel reveals). Feedback: fun and
creative, but overbearing and reads as AI-generated. Goal: cut it back hard — "less is more" —
while keeping a distinct, hand-crafted identity instead of a generic templated one.

Pick one direction below (or tell me which pieces to mix) and I'll implement it.

---

## Option A — Quiet Terminal (keep the identity, cut the noise)

**Concept:** Same technical/terminal DNA, almost none of the machinery. One quiet nod to the
theme (a blinking cursor, `$` prompt-style section labels) instead of a simulated OS.

- **Type:** Single family — IBM Plex Mono (already loaded), 2 weights only (400/600). Drop IBM Plex Sans.
- **Color:** Near-black background (`#0a0e13`), off-white text (`#eef1f6`), **one** accent color
  (keep the pink or drop to plain white — no green/cyan/amber trio, and nowhere near the
  indigo/violet range). Everything else is grayscale, one temperature only (cool grays, not mixed
  warm/cool).
- **Layout:** Single column, generous top/bottom spacing (not side-by-side panels). No rack-rail
  side nav, no LED grid, no rack-unit screw dots, no telemetry dashboard. Section labels become
  plain `$ about`, `$ projects` style prompts — text, not a bordered chip. **Projects section
  becomes a numbered log list** (`01 — Server Architecture & Deployment`, full-width, one per
  line, not boxed) instead of the current 3-card grid — reads more "terminal log" anyway, and
  sidesteps the three-identical-cards tell entirely.
- **Case & type details:** sentence case throughout — drop the current ALL-CAPS treatment on nav
  links and section headings (`ABOUT` → `about`, `U1 / ABOUT.SYS` eyebrow style dropped).
  `text-wrap: balance` on headings, `text-wrap: pretty` on body copy. No drop shadows anywhere —
  separation comes from spacing and 1px hairline rules, not bordered panel chrome.
- **Motion:** Cut entirely: no boot sequence, no canvas matrix rain, no glitch hover, no
  scroll-triggered reveals, no CRT scanline overlay. Keep only a blinking text cursor after the
  name and standard 150ms link/button color transitions, with explicit hover, focus-visible, and
  active states defined (not just hover).
- **What survives:** the live `help`/`fetch`/etc. terminal commands, since that's a genuinely
  interactive feature, not decoration — but it stops being the whole hero, just one quiet element.

---

## Option B — Swiss Editorial (drop the theme entirely)

**Concept:** No terminal concept at all. A plain, confident, content-first resume site — the kind
of restraint that reads as senior, not templated.

- **Type:** Space Grotesk (headings) + Manrope (body) — both loaded via Google Fonts, neither is
  Inter/Roboto/Arial/system-ui, so it doesn't default to the most-flagged AI font choice. Sentence
  case for all headings, buttons, and nav labels — no Title Case, no ALL CAPS.
- **Color:** Light mode. Near-white background (`#fafafa`), near-black text (`#09090b`), one
  accent color used only for links/CTA — pull it from something specific (the current pink,
  desaturated, or a warm ochre/terracotta) rather than a generic "startup blue," and keep it
  nowhere near the indigo/violet range. No gradients, no glow, no multi-color status-LED palette,
  no shadows implying more than one light source.
- **Layout:** Swiss/grid-based: strict column grid, sharp corners (no border-radius), generous
  whitespace, left-aligned headings (never centered), thin hairline rules between sections
  instead of bordered panels. Content is the hierarchy — no card chrome around every block.
  **Projects section is an asymmetric editorial list** — each entry full-width with a hanging
  index number and an offset text column, not three equal-width cards. That also breaks up the
  page rhythm on purpose (About/Stack stay dense two-column, Projects breathes), which is what
  keeps this direction from reading as the rote hero→features→CTA template.
- **Motion:** Near-zero. Subtle 150–200ms hover, focus-visible, and active states on links/buttons
  only. No scroll reveals, no entrance animation, no background effects. `text-wrap: balance` on
  headings, `text-wrap: pretty` on paragraphs.
- **What survives:** none of the terminal gimmicks — this is the "burn it down and start over"
  option.

---

## Option C — Dark Minimal Mono (dark, but no roleplay)

**Concept:** Middle ground — keeps a dark, technical feel without pretending to be an operating
system. Reads as "engineer who likes dark mode," not "hacker terminal cosplay."

- **Type:** Space Mono or JetBrains Mono for headings/labels only, IBM Plex Sans for body copy
  (already part of the current site's identity, and not a banned default like Inter) so long
  paragraphs stay readable. Sentence case throughout — no ALL-CAPS labels.
- **Color:** Monochrome dark (`#111214` background, `#e8e8ea` text), one temperature throughout
  (cool grays only, not mixed), + exactly one accent used only for links and the current section
  indicator — nowhere near the indigo/violet range. No LED color-coding, no term/ok/warn palette,
  no shadows implying more than one light source.
- **Layout:** Single column or simple two-column at most, flat sections separated by hairline
  rules, not bordered/bezeled "rack unit" panels. No side rail, no telemetry grid, no portrait in
  a chrome frame — just the photo, cropped, no border treatment. **Projects section becomes a
  simple numbered list** (same log-style treatment as Option A) instead of a 3-card grid.
- **Motion:** One subtle fade-up on initial page load for the hero only. Nothing scroll-linked.
  Standard hover, focus-visible, and active states elsewhere. `text-wrap: balance` on headings,
  `text-wrap: pretty` on body copy.
- **What survives:** dark mode and monospace-as-accent, which is a real, earned piece of identity
  for a systems-engineering portfolio — just without the boot sequence/rack metaphor carrying the
  whole page.

---

## Cross-cutting cuts (apply regardless of option chosen)

Regardless of which direction you pick, these get removed:
- Boot sequence overlay
- Canvas matrix-rain background
- CRT scanline/flicker effect on the terminal block
- Glitch hover effect on the name
- Rack-rail side navigation with LED status dots
- Bonsai/aquarium/ndsu-ascii terminal easter eggs (fun, but adds to "overbuilt" feeling — cut
  unless you want to keep them deliberately)
- Multi-color status palette (pink/green/cyan/amber) down to one accent
- The current 3-identical-card grid on Projects — every option above replaces it with a list or
  asymmetric layout instead, since "three cards in a row" is one of the most-cited AI tells
- ALL-CAPS uppercase nav links and section headings (`ABOUT`, `U1 / ABOUT.SYS`) — switch to
  sentence case across all three options

---

## Anti-AI-slop rules (binding — check every change against these)

These apply to the redesign implementation itself, not just the direction chosen above. Checked
in order: P0 is a hard blocker, P1 should be fixed, P2 is nice-to-have.

### P0 — cardinal sins, must-fix

1. **No default Tailwind indigo/violet as accent.** Specifically never use `#6366f1`, `#4f46e5`,
   `#4338ca`, `#3730a3`, `#8b5cf6`, `#7c3aed`, `#a855f7`. This is the single most recognizable AI
   tell — use the site's chosen accent instead.
2. **No two-stop "trust" gradient on the hero** (purple→blue, blue→cyan, indigo→pink). A flat
   surface + intentional type beats this every time.
3. **No emoji as feature icons** (✨🚀🎯⚡🔥💡) in headings, buttons, list items, or icon
   containers. If an icon is needed, use a monoline SVG (1.6–1.8px stroke, `currentColor`), not a
   glyph.
4. **No hardcoded Inter/Roboto/system-ui on display text** once a display font is chosen — use it
   consistently for h1/h2, don't silently fall back.
5. **No rounded card with a colored left-border accent** — the canonical "AI dashboard tile"
   shape. Drop either the radius or the left border if a bordered panel is used at all.
6. **No invented metrics** ("10× faster", "99.9% uptime", "3× more productive"). Only real,
   sourced numbers, or don't include a metric at all.
7. **No filler copy** (lorem ipsum, "feature one/two/three", "placeholder text", "sample
   content"). An empty section is a composition problem to solve, not something to paper over
   with fake words.

### P1 — soft tells, should-fix

- Avoid the rote "Hero → Features → Pricing → FAQ → CTA" skeleton with zero variation — at least
  one section should break the pattern (this matters most for Option B, the most conventional
  layout of the three).
- No external placeholder image CDNs (unsplash.com, placehold.co, placekitten.com, picsum.photos).
- Keep raw hex values outside `:root`/CSS custom properties to a minimum (~12 max) — use the
  design tokens, not ad hoc colors scattered through the CSS.
- Cap the single accent color to roughly 2 visible uses per screen — don't let it become wallpaper.

### P2 — polish tells, nice-to-fix

- No decorative blob/wave SVG backgrounds (meaningless geometry with no purpose).
- Avoid a perfectly symmetric layout with zero visual tension — alternating density (one tight
  section, one breathing section) reads as intentional rather than generated.

### Adding soul (not just a ban list)

Aim for ~80% proven/solid patterns + ~20% distinctive choice. The 20% should live in:
- One bold visual move (a typography choice, a single color decision, an unexpected proportion).
- Specific voice/microcopy instead of generic button text ("Open Resume.pdf" beats "Learn More").
- One micro-interaction that's memorable, not decorative (a button press that moves 2px, not a
  bounce/scale).
- One detail that could only exist because Mason actually built/used this (the live terminal
  commands are a good example already — keep something like that).

Test before shipping: if someone screenshotted the finished site, could a stranger tell it's a
specific person's site rather than a generic template? If not, it needs more of the 20%.

---

## Source checklist — general AI-generated design tells

(Moved in from `ai-design-tells.txt`, kept for reference alongside the P0/P1/P2 rules above —
overlapping items like indigo accents, gradients, emoji icons, and invented metrics are already
covered there.)

**Color & gradients**
- Purple-to-blue (or purple-to-cyan) gradients on hero backgrounds, buttons, text, and "orbs" —
  the single most-cited signature
- Indigo/violet as the default accent (Tailwind's indigo-500 / shadcn defaults)
- Radial "glow" gradients floating behind headings or icons
- Gradient text (headline text itself rendered in a color gradient)

**Glassmorphism / depth effects**
- Frosted-glass cards (blur + transparency) floating over a gradient or dark background
- A thin, glowing 1px border combined with a soft drop shadow — "neon glass"
- Cards nested inside cards inside cards, each with their own padding/shadow

**Layout & components**
- Three (or four) feature cards in a row, each: icon, bold heading, exactly two lines of body text
- A thick colored border/accent on just one side of a rounded card
- One big rounded icon (often a Lucide/Heroicons glyph) centered above a heading
- Everything in a rounded-corner card, even when there's no reason to group it
- Excessive whitespace/padding used to look "clean" rather than to serve hierarchy

**Typography**
- Inter (or similar geometric sans) in every weight, used everywhere
- All-caps, wide letter-spacing "eyebrow" labels above headings
- Overuse of bold for emphasis rather than actual hierarchy

**Motion / interaction**
- Hover bounce/scale animations on cards and buttons that serve no purpose
- Fade/slide-in scroll animations on every section
- Shimmer/pulse loading effects used decoratively rather than functionally

**Iconography & imagery**
- Emoji used as section icons instead of a real icon set
- Generic abstract 3D blobs/orbs as decoration
- Stock "gradient mesh" background textures

**Copy / microcopy**
- Buzzword-dense, vague marketing copy ("Unlock your potential," "Seamlessly integrate")
- Fake specificity for flavor (made-up version numbers, "protocol" jargon) with no real meaning

**Structure & copy patterns**
- shadcn/ui defaults everywhere — buttons/cards/badges that look identical across unrelated projects
- The "trusted by" logo strip — row of grayscale company logos under the hero, almost always fabricated
- Full formulaic page stack: nav → hero → logo strip → 3-feature grid → testimonial carousel →
  pricing table → FAQ accordion → final CTA banner → 4-column footer
- Generic CTA copy — "Get Started" / "Learn More" side by side, "Start Free Trial"
- Checkmark bullet lists — green circle + checkmark icon in front of every feature bullet
- Numbered step circles connected by a line, for any "how it works" section
- Avatar stack + star rating near a CTA
- "New" badge pill top-left of the hero, usually meaningless
- Backdrop-blur sticky navbar
- Everything center-aligned, even when left-aligned would read better
- Oversized font-weight (800/900) headlines paired with a much lighter body font
- Decorative monospace used outside of actual code context

*(Original note on this list mentioned an old `form.html` that no longer exists in this project —
no longer applicable, kept the rest for reference.)*

Sources: [mohitphogat.medium.com](https://mohitphogat.medium.com/ai-design-slop-why-every-ai-built-interface-looks-the-same-and-how-to-fix-it-bf874e0b470c),
[dev.to/alanwest (indigo-500)](https://dev.to/alanwest/why-every-ai-built-website-looks-the-same-blame-tailwinds-indigo-500-3h2p),
[925studios.co](https://www.925studios.co/blog/ai-slop-design-tells),
[impeccable.style/slop](https://impeccable.style/slop/)

---

## Source checklist — "How to stop your frontend looking AI-generated" (Medium, Jacob Perks, Aug 2026)

New/specific items this article adds that the lists above don't already cover:

**Typography**
- Swap away from Inter / Roboto / Arial / Open Sans / Helvetica toward something like Geist,
  Manrope, or Poppins (Geist Mono for the monospace slot). Avoid italics and any weight beyond
  bold.
- Use sentence case for headings, buttons, and labels — not Title Case or ALL CAPS by default.
- `text-wrap: balance` on headings, `text-wrap: pretty` on paragraphs, to kill orphaned words.
- Concentric border-radius formula for nested rounded elements: inner radius = outer radius − gap,
  so nested corners actually look concentric instead of arbitrary.

**Color & surfaces**
- If texture is wanted instead of a flat gradient, use subtle film grain (SVG `feTurbulence` at
  ~0.06–0.16 opacity) rather than a gradient mesh.
- Sample palettes from a real, specific reference (a physical object, a photo) rather than
  defaulting to generic "startup blue."
- Keep one color temperature site-wide — don't mix warm and cool greys.
- Limit to one accent color for the whole site (already consistent with the P1 "≤2 uses per
  screen" rule above).
- Avoid shadows that imply multiple light sources (i.e. don't stack shadows going in different
  directions on the same element).

**Layout**
- Instead of "three identical cards in a row," use a bento grid, an icon list, or alternating
  image/text blocks.
- Avoid perfectly centering everything — offset copy, anchor images to the bottom of their
  container instead of vertically centering.
- Avoid making every grouping exactly three items by reflex.
- Don't wrap every content block in a card — background color or spacing alone is often enough.
- If using a card grid, standardize header heights, use `min-height` on descriptions and
  `margin-top: auto` on buttons so cards align instead of visibly drifting.
- Use `min-height: 100dvh` instead of `height: 100vh` (fixes mobile Safari viewport jump).

**Copy**
- Avoid em dashes in body copy (use periods instead).
- Avoid overused verbs like "elevate" and "seamless."
- Avoid placeholder company/product names (e.g. "Acme Corp") and fabricated
  testimonials/social proof.

**Icons & imagery**
- Skip the obvious default icon sets (Lucide/Feather) paired with the predictable metaphor for the
  concept (e.g. a rocket for "launch") — that pairing itself reads as generated.

**Accessibility (non-negotiable, not just a "nice to have")**
- `<header>`, `<main>`, and the footer landmark should be siblings, never nested inside each other.
- Anything that auto-moves for more than ~5 seconds needs a pause control (`aria-pressed` button).
- Wrap animation with a `prefers-reduced-motion` fallback.
- Prefer `IntersectionObserver` over raw scroll listeners for any scroll-triggered behavior.
- Implement all real interactive states: hover, active, focus, loading, empty, and error — not
  just default and hover.

**Review process to run before calling the redesign done**
Do six separate passes rather than one pass eyeballing the whole page: accessibility, layout,
typography, color, writing, general UI. Rank each finding High (misleads/fabricates/reads as
obviously AI-generated) / Medium (meaningfully hurts quality) / Low (isolated polish), then fix in
this order: font → color & surfaces → interaction states → layout & spacing → motion → generic
components → empty/error states → copy → type-scale polish. Fix the highest-impact, lowest-risk
items first.

Source: [Jacob Perks — "How to stop your frontend looking AI-generated"](https://medium.com/design-bootcamp/how-to-stop-your-frontend-looking-ai-generated-efbb9681a6a2)

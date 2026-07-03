# Anti-AI Design — What Makes a Website Look AI-Generated

A diagnostic catalog of the tells that scream "an AI made this." Read it as a
pre-flight checklist: before shipping any UI, scan for these patterns and remove
them. This is the companion to `design-direction.md` — that file says what *to* do;
this file says what to *stop* doing, and why it reads as amateur.

**Rule of thumb:** AI-generated UI fails by being *generic, loud, and uniform*.
Premium UI is *specific, calm, and hierarchical*. Every anti-pattern below is a
lapse into generic/loud/uniform.

> Format for each entry: **Why it looks amateur → Fix (with the better alternative).**

---

## 1. Common AI Design Mistakes

The signature combo: purple-blue gradients, three equal feature cards with emoji,
centered everything, oversized radius, and heavy shadows. Individually survivable;
together they are a fingerprint.

- **Why it looks amateur:** it's the statistical average of a million templates —
  zero point of view, zero hierarchy, instantly recognizable as machine output.
- **Fix:** commit to one specific direction (see `design-direction.md` inspiration
  brands) and enforce restraint — a near-monochrome layout, one confident accent, a
  decisive type scale, and one clear focal point per screen.

## 2. Poor Spacing Patterns

Uniform padding on everything, arbitrary values (`p-[13px]`), cramped fields, and
sections with no breathing room.

- **Why it looks amateur:** uniform spacing erases grouping cues — the eye can't tell
  what belongs together. Off-grid values look accidental.
- **Fix:** snap everything to a 4px grid and use *rhythm* — tight gaps for related
  items (`gap-2`/`space-y-4`), large gaps between groups (`gap-8`+), `py-16`–`py-24`
  between page sections. Let proximity signal relationship before any border does.

## 3. Bad Typography

One font size for everything, thin 300 weights, gradient-filled headings, centered
paragraphs running edge-to-edge, three+ font families.

- **Why it looks amateur:** flat type = no hierarchy; the reader has no guide.
  Gradient text and thin weights read as decorative gimmicks, not craft.
- **Fix:** decisive scale (body 16, headings jumping to 30/36/48+), weights
  400/500/600, solid `foreground` color, tracking tightened on big headings; max two
  families (one sans + one mono), left-aligned body capped at ~65–75ch, `tabular-nums`.

## 4. Weak Hierarchy

Every element demanding equal attention — same size, same weight, same color,
multiple "primary" buttons competing.

- **Why it looks amateur:** with no focal point the page feels like a list of parts,
  not a designed whole. Users don't know where to look or what to do.
- **Fix:** pick ONE primary action per view and establish rank via
  size → weight → color → space (color last); everything secondary visibly recedes
  (`muted-foreground`, `ghost`/`outline`) so one high-contrast element leads.

## 5. Overused Gradients

Purple→pink or blue→teal hero backgrounds, gradient buttons, gradient text, gradient
borders — gradients as the whole personality.

- **Why it looks amateur:** it's the #1 AI tell. Saturated multi-hue gradients look
  cheap, date instantly, and fight the content for attention.
- **Fix:** default to a flat `--background` with one accent; if you use a gradient,
  make it *one*, subtle, low-saturation, and supporting — a barely-there monochrome
  mesh used once (Stripe-style), never a full-page rainbow.

## 6. Generic Hero Sections

Centered headline + centered subtext + one big CTA + a gradient blob or stock
illustration behind it.

- **Why it looks amateur:** it's the default template hero — interchangeable across
  ten thousand sites, communicating nothing specific about the product.
- **Fix:** lead with a specific, concrete value proposition; a confident large
  heading, one supporting line, a single primary action, and a real product visual
  (screenshot) with layered depth. Left-align for an editorial, content-first feel.

## 7. Generic Feature Cards

Three identical cards in a row, each with an emoji/icon on top, a bold title, and two
lines of filler — all equal weight.

- **Why it looks amateur:** perfect uniformity signals "filled a template." No card
  is more important than another, so none feels important.
- **Fix:** break the grid into an asymmetric bento where the flagship feature gets
  more space, supported by smaller ones; consistent Lucide icons at one size, no
  emoji, and specific copy instead of filler.

## 8. Emoji Abuse

Emoji in headings, buttons, section titles, and as UI icons (Fast, Beautiful,
Secure with rocket/sparkle/lock glyphs).

- **Why it looks amateur:** emoji-as-icons is an instant tell of low effort —
  inconsistent rendering across platforms, no visual coherence, toy-like tone.
- **Fix:** replace every emoji with a proper icon from one set (`<Zap />`,
  `<Shield />`, `<Sparkles />`) at 16–20px, muted by default — coherent, professional,
  and cross-platform-stable.

## 9. Poor Icon Usage

Mixed icon libraries, inconsistent sizes and stroke widths, icons replacing text
without labels, oversized decorative icons.

- **Why it looks amateur:** mismatched icons look assembled from clip-art; icon-only
  controls with no label are a usability and a11y failure.
- **Fix:** commit to one library (Lucide), one size system (16px dense / 20–24px
  standalone) and uniform stroke; pair icon + label with `gap-2`, use `currentColor`,
  and allow icon-only only with a tooltip and `aria-label`.

## 10. Excessive Shadows

Heavy, dark, high-spread drop shadows on every card, button, and input — sometimes
stacked with thick borders.

- **Why it looks amateur:** loud shadows look like early-2010s skeuomorphism; on
  everything, they create noise and flatten hierarchy (nothing stands out if
  everything floats).
- **Fix:** use soft, low-spread `shadow-sm` sparingly for genuine elevation and let
  hairline `border`s do most separation; no shadow on inputs, and reserve stronger
  elevation for true overlays (popovers, dialogs).

## 11. Excessive Border Radius

Huge rounded corners on everything (`rounded-3xl` buttons, pill-shaped cards),
inconsistent radii across the same surface.

- **Why it looks amateur:** oversized radius reads as bubbly and unserious; mixed
  radii look careless and off-brand.
- **Fix:** pick one moderate radius system and hold it — `rounded-lg`/`rounded-xl` on
  cards, `rounded-md` on buttons/inputs — applied consistently. Precision reads as
  premium.

## 12. Bad Color Combinations

Rainbow of accent colors, fully saturated backgrounds, low-contrast text on tinted
surfaces, random hex values hardcoded per component.

- **Why it looks amateur:** many competing hues have no semantic meaning and fight
  each other; saturated backgrounds strain the eye; hardcoded colors break theming.
- **Fix:** ~90% neutral grayscale ramp + ONE restrained accent in `oklch`, with extra
  hue only for semantic status (success/warning/destructive/info); route all color
  through shadcn CSS variables so theming and dark mode stay consistent.

## 13. Weak CTA Design

CTAs that blend into the page, multiple competing "primary" buttons, vague labels
("Click here", "Submit", "Learn more"), no hover/focus feedback.

- **Why it looks amateur:** if the main action isn't obvious, the design has failed
  its one job; vague verbs give users no reason to act.
- **Fix:** exactly one visually dominant solid-accent primary per view with a
  verb-first, specific label ("Start free trial", "Create project"); demote secondary
  actions to `ghost`/`outline`; include the full state set (hover, focus, active, loading).

## 14. Generic Dashboards

Four identical stat cards across the top, a sidebar of icons, one big chart, and
uniform padding — the "admin template" look.

- **Why it looks amateur:** it's a numbers-by-the-yard layout with no point of view;
  every metric weighted equally means no insight is surfaced.
- **Fix:** prioritize into a hierarchy-driven bento (hero metric + supporting KPIs + a
  focused chart), `tabular-nums` for figures, hairline table separators, skeleton
  loading and designed empty states, and quiet chrome.

## 15. Poor Mobile Layouts

Desktop layouts crammed onto phones, tiny tap targets, horizontal scroll, text at the
screen edge, nav that doesn't collapse.

- **Why it looks amateur:** it signals mobile was an afterthought; cramped, unusable
  touch UX erodes trust immediately.
- **Fix:** design mobile-first (works at 360px) as a fluid single column with `clamp()`
  type, touch targets ≥44px, thumb-reachable primary actions, nav collapsed to a
  sheet/drawer, and columns introduced only at `md`/`lg`.

## 16. Accessibility Mistakes

Removed focus outlines, color-only state, low-contrast muted text, missing labels,
`<div onClick>` instead of `<button>`, no reduced-motion handling.

- **Why it looks amateur:** beyond excluding users, these are craft failures pros
  never ship — invisible focus and unreadable text look broken to everyone.
- **Fix:** keep visible `focus-visible` rings, hit WCAG contrast (4.5:1 body), pair
  color with icon/text, label every input (`aria-describedby` errors), and use
  semantic HTML (`<button>`/`<nav>`/`<main>`, ordered headings). See `accessibility.md`.

## 17. Motion Mistakes

Everything animating, long showy transitions, animating `width`/`height`/`top`,
parallax everywhere, five different easing curves, motion that ignores reduced-motion.

- **Why it looks amateur:** gratuitous motion feels like a demo reel, distracts from
  content, and janky layout-property animation stutters on real devices.
- **Fix:** animate only `transform`/`opacity`, 150–250ms, ease-out, on purposeful
  moments (state change, entrance, feedback) with one easing token — a subtle fade on
  menu open, a gentle button press — and cut it under `prefers-reduced-motion`.

## 18. Empty Whitespace Usage

Two failure modes: (a) cramming everything with zero breathing room, or (b) vast
meaningless voids with a lonely centered element and no rhythm.

- **Why it looks amateur:** cramped UI feels cheap and stressful; aimless emptiness
  feels unfinished. Both show space wasn't *designed*, just left over.
- **Fix:** treat space as a material — confident margins around headings and sections,
  tight internal grouping of related content, and no region left empty merely because
  it exists.

## 19. Over-Engineered UI

Glassmorphism + heavy shadows + gradients + animations + 3D + neon glow all at once;
decorative complexity with no functional purpose.

- **Why it looks amateur:** piling on effects is what beginners do to look "advanced";
  it produces noise, hurts performance, and buries the content.
- **Fix:** subtract to a calm, flat layout with one restrained accent and at most one
  cleanly-executed signature treatment — every effect must earn its place by aiding
  comprehension. Restraint reads as confidence.

## 20. Visual Clutter

Too many competing elements, borders around everything, dividers between every item,
badges and pills everywhere, decorative lines and dots.

- **Why it looks amateur:** clutter has no hierarchy — the eye can't rest or find the
  important thing. Boxes-within-boxes look like a wireframe, not a product.
- **Fix:** remove borders that space can replace and group with whitespace first;
  reserve badges for genuine status and delete decorative elements that carry no
  information — nothing on screen without a reason.

---

## Quick Detection Checklist

The single authoritative pre-ship list. If a generated design has **any** of these,
revise before shipping:

- [ ] Purple/blue (or any multi-hue) gradient background or gradient text
- [ ] Three+ identical feature cards in a uniform row
- [ ] Emoji used as icons or in headings/buttons
- [ ] Everything centered; no left-aligned reading content
- [ ] More than one "primary" button competing per view
- [ ] Heavy drop shadows and/or thick colored borders on cards
- [ ] Oversized or inconsistent border radius
- [ ] More than one accent hue (excluding semantic status colors)
- [ ] Hardcoded hex colors instead of shadcn CSS variables
- [ ] Flat type scale / thin 300 weights / three+ font families
- [ ] Uniform padding everywhere; off-grid arbitrary spacing values
- [ ] Removed focus outlines or color-only state indication
- [ ] Gratuitous or layout-property animation; no reduced-motion support
- [ ] Desktop layout not adapted for 360px mobile; sub-44px tap targets
- [ ] Generic centered hero with a gradient blob and a stock illustration
- [ ] Mixed icon libraries or inconsistent icon sizes/strokes
- [ ] "Lorem ipsum" or filler copy left in the output

> If the answer to *"could this be any product?"* is yes, it's too generic. Premium
> UI is specific. Remove the tells above until the design could only belong to *this*
> product — then it no longer looks AI-generated.

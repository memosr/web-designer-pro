# Design Direction — Web Designer Pro

The visual philosophy of Web Designer Pro. This is the taste layer on top of the
mechanical shadcn knowledge in the other references. Where `components.md` says
*how* to install a button, this document says *what a button should feel like*.

**North star:** every generated surface should read like it came from Stripe,
Linear, Apple, Vercel, Notion, or Raycast — never like a generic AI template.
When a decision is ambiguous, choose the option those teams would ship.

> This file defines intent. Apply it alongside `theming-and-dark-mode.md` (tokens),
> `composition-patterns.md` (layout), and `accessibility.md` (a11y).

---

## Design Philosophy

Five principles govern every choice. In conflicts, earlier principles win.

1. **Restraint over decoration.** Nothing on screen without a reason. Remove until
   it breaks, then add one thing back. The best UI is mostly empty space.
2. **Hierarchy over uniformity.** One clear focal point per view. If everything is
   emphasized, nothing is. Guide the eye deliberately.
3. **Content is the interface.** Chrome recedes; the user's data is the hero.
   Borders, shadows, and fills are servants, not stars.
4. **Precision over approximation.** Aligned to a grid, consistent radii, tokenized
   color. Sloppiness reads as "AI-generated" faster than anything else.
5. **Calm over loud.** Muted palettes, soft motion, quiet defaults. Save saturation
   and animation for the single moment that matters.

> If a screen looks "designed," you've likely overdone it. Aim for *inevitable*.

## Inspiration Brands

Reference the specific quality each brand is known for. Do not clone; internalize.

| Brand | Steal this |
|-------|-----------|
| **Stripe** | Layered depth, generous white space, precise typography, subtle gradients used with discipline |
| **Linear** | Speed-feel, keyboard-first density, near-monochrome palette, hairline borders, restrained purple accent |
| **Apple** | Type-driven hierarchy, huge headings, immaculate spacing rhythm, product-as-hero |
| **Vercel** | Pure black/white contrast, geometric clarity, confident negative space, mono for technical detail |
| **Notion** | Warm neutrals, comfortable reading measure, soft edges, content-first calm |
| **Raycast** | Dark-mode craft, tight command-menu density, crisp iconography, tactile micro-interactions |

**The through-line:** neutral base, one restrained accent, real typographic
hierarchy, and space used as a material. None of them ship rainbow gradients,
purple-to-pink hero blobs, or emoji-in-headings.

## Visual Hierarchy

Establish rank through **size → weight → color → space**, in that order of
preference. Reach for color last.

- **One primary action per view.** Everything else is secondary or tertiary.
- **Three levels of text emphasis, max:** primary (foreground), secondary
  (muted-foreground), tertiary (muted-foreground at smaller size). No more.
- **Contrast creates focus.** A single high-contrast element in a calm field draws
  the eye. Scatter contrast and the page goes flat.
- **Size ratios should be decisive.** A heading that's only slightly larger than
  body text reads as a mistake. Jump confidently (see type scale).

```
Emphasis ladder (strongest → weakest):
  Display heading   → largest, tight tracking
  Section heading   → clear step down
  Body              → comfortable, foreground
  Meta / caption    → muted-foreground, smaller
  Disabled / hint   → lowest contrast
```

## Typography

Type is the primary design tool. Most of the "premium" feeling is typographic.

**Font choices**
- **Sans-serif UI:** Inter, Geist, or the system stack. These are the safe,
  professional defaults. `font-family: var(--font-sans)`.
- **Monospace:** Geist Mono, JetBrains Mono, or SF Mono for code, IDs, metrics,
  and technical values — used deliberately, à la Vercel/Linear.
- **Max two families.** One sans + one mono. Never more. No decorative display fonts.

**Type scale** (major-third-ish, decisive steps — not 15 sizes)

| Token | Size | Use |
|-------|------|-----|
| `text-xs` | 12px | meta, captions, table labels |
| `text-sm` | 14px | secondary UI, dense tables, form hints |
| `text-base` | 16px | body, default |
| `text-lg` | 18px | lead paragraphs |
| `text-xl`–`2xl` | 20–24px | card titles, subsection headings |
| `text-3xl`–`4xl` | 30–36px | section headings |
| `text-5xl`+ | 48px+ | hero / display |

**Rules**
- **Weight:** 400 body, 500 for emphasis/labels, 600 for headings. Reserve 700+
  for display only. Avoid 300 — thin weights read as fragile.
- **Tracking:** tighten large headings (`-0.02em` to `-0.03em`); leave body at
  default; slightly loosen all-caps micro-labels (`+0.05em`).
- **Line-height:** ~1.5 for body, ~1.1–1.2 for large headings.
- **Measure:** cap reading columns at ~65–75ch (`max-w-prose`). Never let paragraphs
  run edge-to-edge.
- **Numbers:** use `tabular-nums` (font-variant-numeric) in tables and metrics so
  digits align.

> Anti-generic tell: gradient text on headings and inconsistent heading sizes.
> Ship solid `foreground` color and a disciplined scale instead.

## Spacing System

Space is a designed material, not leftover gap. Everything sits on a **4px base
grid** (Tailwind's default: `1` = 4px).

- **Use the scale:** 4, 8, 12, 16, 24, 32, 48, 64, 96. Prefer these steps; avoid
  arbitrary values like `p-[13px]`.
- **Rhythm, not uniformity.** Related elements sit close (`gap-2`/`gap-3`);
  distinct groups get real separation (`gap-8`+). Uniform padding everywhere is a
  template smell.
- **Section spacing scales with viewport:** generous vertical breathing room between
  page sections (`py-16` to `py-24`+ on marketing surfaces).
- **Inside components stays tight and consistent:** card padding `p-6`, form field
  gaps `space-y-4`, button padding proportional to size.
- **Proximity = relationship.** A label glued to its input, an input separated from
  the next field. Let spacing communicate structure before borders do.

## Color Principles

**Palette architecture: neutral-dominant, single accent.**

- **~90% neutral.** Backgrounds, surfaces, borders, and most text live in a grayscale
  ramp. This is what makes Stripe/Linear/Vercel look expensive.
- **One accent color** for primary actions, active states, and focus. Introduce a
  second (semantic) hue only for status: success, warning, destructive, info.
- **Never hardcode color.** Always use the shadcn CSS variables so light/dark and
  theming Just Work.

```css
/* Always reference tokens, never literals */
background: var(--background);
color: var(--foreground);
border-color: var(--border);
/* accent */
background: var(--primary);
color: var(--primary-foreground);
```

- **Use `oklch`** for all custom colors (perceptually uniform lightness) — matches
  modern shadcn. See `theming-and-dark-mode.md`.
- **Borders are near-invisible.** Hairline separators at low contrast (`--border`),
  not heavy 2px lines.
- **Saturation is a spice.** Muted, desaturated tones for surfaces; save chroma for
  the one accent. Fully saturated backgrounds read as amateur.
- **Semantic mapping:** destructive = red family, success = green, warning = amber,
  info = the accent or blue. Consistent across the whole app.

> Anti-generic tell: purple→pink or blue→teal gradient backgrounds. Ship a flat,
> tokenized neutral surface with a single accent instead.

## Layout Rules

- **Grid-based, consistent max-width.** Content containers use a shared
  `max-w-*` + centered `mx-auto` with responsive horizontal padding
  (`px-4 sm:px-6 lg:px-8`).
- **12-column mental model** for complex pages; align everything to it.
- **Asymmetry with intent.** Editorial/bento compositions beat endless identical
  card grids — but only when hierarchy justifies it.
- **Optical alignment over mathematical** when they disagree (icons, quotes).
- **Consistent gutters and consistent radii** across the whole surface. Mixed corner
  radii is a top template tell.
- **Above the fold earns its keep:** clear value, one primary action, no clutter.
- **Don't center everything.** Left-aligned text is easier to read; reserve centering
  for short hero copy and empty states.

## White Space

White space is not emptiness — it's the product looking confident.

- **Be generous.** When unsure, add more space, not more elements.
- **Let hero and section headings breathe** with large surrounding margins.
- **Density is contextual:** marketing = spacious; data tables/command menus = tight
  but still rhythmic.
- **Never fill space just because it exists.** An empty region is a valid design.
- **Group with space before you group with lines.** Reach for a divider only when
  spacing alone can't carry the structure.

## Cards

The default container — get these right and most of the UI looks right.

- **Surface:** `bg-card` on `bg-background`, separated by a **hairline border**
  (`border`) and/or a **very soft shadow** — rarely both loud.
- **Radius:** consistent, moderate (`rounded-lg` / `rounded-xl`). Pick one and hold
  it everywhere.
- **Padding:** roomy and uniform (`p-6`). Internal `space-y-*` for rhythm.
- **Shadows:** subtle and low-spread (`shadow-sm`), used for gentle elevation, not
  drama. Stack shadows sparingly for Stripe-style depth.
- **Hover (when interactive):** a slight border/shadow lift or `bg-accent/50` — never
  a jarring transform.

```tsx
<Card className="rounded-xl border bg-card shadow-sm transition-shadow hover:shadow-md">
  <CardHeader className="p-6">
    <CardTitle className="text-lg font-semibold tracking-tight">Title</CardTitle>
    <CardDescription className="text-sm text-muted-foreground">Supporting line</CardDescription>
  </CardHeader>
  <CardContent className="p-6 pt-0">…</CardContent>
</Card>
```

> Anti-generic tell: heavy drop shadows + thick colored borders + oversized radius.
> Dial all three down.

## Buttons

- **One primary per view.** Solid `--primary` fill, `--primary-foreground` text.
- **Hierarchy of variants:** `default` (primary) → `secondary`/`outline` → `ghost`
  → `link`. Secondary actions must visibly recede.
- **Sizing:** proportional padding, comfortable tap target (min 40px height for
  primary; `size="sm"` for dense toolbars).
- **States are non-negotiable:** distinct hover, `focus-visible` ring, active
  (slight scale/darken), disabled (reduced opacity, no pointer). All four.
- **Labels:** verb-first, sentence case, concise ("Create project", not "Click here
  to create a new project now").
- **Loading:** show a spinner + disable, keep width stable to avoid layout shift.
- **Icons:** optional leading icon, consistent size (16px), proper gap (`gap-2`).

```tsx
<Button className="transition-colors focus-visible:ring-2 focus-visible:ring-ring">
  Create project
</Button>
```

## Forms

Forms are where premium products quietly win trust. Use RHF + Zod (`forms.md`).

- **Vertical, single-column** by default. Two columns only for genuinely paired fields.
- **Label above input**, `text-sm font-medium`. Clear, human labels.
- **Comfortable field spacing:** `space-y-4` between fields, never cramped.
- **Inline validation, on blur/submit**, not aggressively on every keystroke.
- **Error text below the field** in `--destructive`, specific and actionable
  ("Enter a valid email", not "Invalid input").
- **Helper/hint text** in `muted-foreground` under the field.
- **Focus states obvious:** a clear `ring` on the active input.
- **Group related fields** with spacing or subtle section headings; don't wall
  everything in boxes.
- **Primary submit is prominent; cancel is `ghost`/`outline`.** Never two primaries.
- **Disable submit while pending**, show progress, prevent double-submit.

## Tables

Data density done with restraint (see `data-tables.md` for mechanics).

- **Whitespace, not gridlines.** Horizontal hairline row separators only; avoid full
  cell borders and zebra stripes unless density truly demands them.
- **Left-align text, right-align numbers.** Use `tabular-nums`.
- **Column headers:** `text-xs`/`text-sm`, `muted-foreground`, medium weight, often
  uppercase with slight tracking.
- **Comfortable row height** (`h-12`-ish); dense mode is opt-in.
- **Row hover:** subtle `bg-muted/50` for scan-ability.
- **Sticky header** on scroll for long tables.
- **Actions:** icon buttons or a trailing `⋯` menu, revealed/settled on hover, never
  a wall of buttons per row.
- **Empty, loading, error states are designed**, not blank: skeleton rows while
  loading, a helpful empty state with a primary action.

## Navigation

- **Sidebar or top nav, not both loud.** Pick a primary structure.
- **Clear active state** (accent text/indicator + subtle background), obvious hover.
- **Keyboard-first mindset:** support a command menu (`⌘K`) for app surfaces —
  the Raycast/Linear signature.
- **Persistent, quiet chrome.** Nav recedes; content leads.
- **Breadcrumbs** for depth; keep them small and muted.
- **Icons + labels** in sidebars; icon-only only when space-constrained (with
  tooltips). Consistent icon set and size.
- **Mobile:** collapse to a sheet/drawer, not a cramped desktop nav.

## Motion

Motion clarifies; it never performs. Restraint is the whole game.

- **Fast and subtle:** 150–250ms for most transitions; ease-out for enters.
- **Animate compositor-friendly properties only:** `transform` and `opacity`.
  Never animate `width`/`height`/`top`/`left` for interactions.
- **Purposeful only:** state changes, entrances/exits, feedback. No decorative
  loops, no parallax-for-parallax's sake.
- **Micro-interactions on real actions:** button press, toggle, menu open, toast in.
- **Stagger lists gently** (small delay) when several items enter at once.
- **Respect `prefers-reduced-motion`:** cut or reduce animation, never break usability.
- **Consistent easing tokens** across the app; don't mix five curves.

```css
transition: transform 200ms cubic-bezier(0.16, 1, 0.3, 1),
            opacity 200ms ease-out;
@media (prefers-reduced-motion: reduce) { transition: none; }
```

## Icons

- **One coherent set** — Lucide (ships with shadcn) is the default. Don't mix icon
  libraries.
- **Consistent size and stroke:** 16px in dense UI, 20–24px standalone; uniform
  stroke width.
- **Icons support text, rarely replace it.** Icon-only needs a tooltip + `aria-label`.
- **Optical sizing and alignment:** vertically center with adjacent text (`gap-2`).
- **Muted by default**, inherit `currentColor`, brighten on hover/active.
- **No emoji as UI icons.** Ever. (See anti-patterns.)

## Dark Mode

A first-class mode, not an inverted afterthought (see `theming-and-dark-mode.md`).

- **Not pure black.** Use a very dark neutral surface (`oklch(~0.14 0 0)`) with
  slightly lighter elevated surfaces — the Raycast/Linear approach. Pure `#000`
  looks cheap and causes halation.
- **Elevation via lightness,** not heavy shadows: higher surfaces are subtly lighter.
- **Lower text contrast slightly** vs light mode to avoid glare, but stay within WCAG.
- **Desaturate accents a touch** so they don't vibrate on dark surfaces.
- **Borders get lighter, not darker,** to remain visible.
- **Test both modes for every component.** Both must feel intentional and equally
  polished — dark mode is not a `filter: invert()`.
- **Respect system preference** (`next-themes`, `defaultTheme="system"`), offer a toggle.

## Mobile First

- **Design the small screen first,** then enhance up. Content and primary action must
  work at 360px wide.
- **Touch targets ≥ 44×44px.** Space interactive elements so fingers don't collide.
- **Single-column by default;** introduce columns at `md`/`lg` only when they help.
- **Reachability:** primary actions within thumb reach; consider bottom sheets/bars.
- **No horizontal scroll** (except deliberate carousels/tables with clear affordance).
- **Fluid type and spacing** via `clamp()` where it earns its keep.
- **Test the real breakpoints:** 360, 390, 768, 1024, 1440.

## Accessibility

Non-negotiable and part of "premium" — see `accessibility.md` for shadcn specifics.

- **Contrast:** body text ≥ 4.5:1, large text/UI ≥ 3:1. Muted text still must pass.
- **Visible focus** on every interactive element (`focus-visible:ring`). Never remove
  outlines without a replacement.
- **Full keyboard operability:** logical tab order, Escape closes overlays, arrow keys
  in menus. shadcn/Radix gives most of this — don't break it.
- **Semantic HTML first:** real `<button>`, `<nav>`, `<main>`, headings in order.
- **Label every input;** associate errors with fields (`aria-describedby`).
- **Don't rely on color alone** to convey state — pair with icon/text.
- **Respect `prefers-reduced-motion`** and `prefers-color-scheme`.
- **Alt text** on meaningful images; `aria-hidden` on decorative ones.

## Premium UI Patterns

The details that separate Stripe/Linear-tier work from generic output.

- **Layered depth:** stacked soft shadows + subtle borders + faint gradients for
  quiet dimensionality (Stripe). Restraint is what sells it.
- **Command menu (`⌘K`):** fast, fuzzy, keyboard-driven navigation/actions.
- **Skeleton loading:** shaped placeholders that match final content — no spinners
  for whole pages, no layout shift.
- **Designed empty states:** a line of guidance + one primary action, not a blank box.
- **Optimistic UI:** reflect the action instantly, reconcile on response.
- **Toasts for feedback:** concise, auto-dismiss, bottom/top-corner, non-blocking.
- **Keyboard shortcuts** surfaced in tooltips and menus.
- **Inline editing** where it removes a modal.
- **Tabular numerals** for any aligned figures.
- **Subtle gradient/mesh accents** used once, quietly — never as a full-page backdrop.
- **Micro-copy with a voice:** clear, calm, occasionally warm — never corporate filler.

## Anti-Patterns (NEVER generate)

The fastest tells of AI-generated / template UI have their own catalog — each with why
it looks amateur and the concrete fix.

> See **`anti-ai-design.md`** for the full anti-pattern catalog and detection checklist.

## Final Design Checklist

Core recap — the design stands on these five disciplines:

- [ ] ~90% neutral palette + one accent, all via shadcn `oklch` tokens
- [ ] Decisive type hierarchy; max two font families; solid (not gradient) text
- [ ] 4px spacing rhythm with generous, intentional white space
- [ ] Full interactive states (hover, `focus-visible`, active, disabled) + WCAG contrast
- [ ] Intentional dark mode; mobile-first (works at 360px, touch targets ≥44px)

> For the complete pre-ship verification list, use the detection checklist in
> **`anti-ai-design.md`**. Final gut-check: would this look at home next to Stripe,
> Linear, or Vercel? If not, it's not done.

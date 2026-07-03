---
name: web-designer-pro
description: >
  This skill should be used for modern web design and UI work — whenever the user
  asks to build or improve a "landing page", "marketing website", "SaaS app",
  "dashboard", "admin panel", "web3 interface", "portfolio website", or requests a
  "UI redesign", "UI improvements", "premium UI", "modern UI", or "beautiful UI".
  It also covers shadcn-specific requests: "add a shadcn component",
  "create a form with shadcn", "build a dashboard with shadcn", "add a data table",
  "configure shadcn ui", "set up dark mode with shadcn", "create a chart with shadcn",
  "use shadcn blocks", "theme a next.js app with shadcn", "install shadcn ui",
  "add a sidebar", "create a login page with shadcn", or when building any
  Next.js application that uses Shadcn UI components, Radix UI primitives,
  or Tailwind CSS-based component patterns.
allowed-tools: Read, Bash, Glob, Grep
metadata:
  version: 2.0.0
---

# Shadcn UI for Next.js

## Overview

Shadcn UI is a collection of re-usable components built on Radix UI and Tailwind CSS. It is **not an npm package** — instead, a CLI copies component source code directly into the project at `components/ui/`. This gives full ownership and control over every component. All components are accessible by default (via Radix), styled with Tailwind CSS, and composable.

**Official docs:** https://ui.shadcn.com

## Design Direction

This skill covers both the **mechanics** (how to install and wire up shadcn) and the
**taste** (what the result should look like). The taste layer lives in
**`references/design-direction.md`** — a visual philosophy that makes generated
interfaces read like Stripe, Linear, Apple, Vercel, Notion, and Raycast instead of a
generic AI template.

Read the design layer *before* generating markup, then apply its principles
(neutral-dominant palette + single accent, decisive typographic hierarchy, 4px
spacing rhythm, restraint over decoration) on top of the shadcn patterns in the rest
of this skill. Two reference files make up this layer — load them by the rules below,
not automatically. This keeps the progressive-disclosure architecture intact: only
pull in what the task needs.

### Load `references/design-direction.md` when:

- Creating a complete website
- Landing pages
- Marketing pages
- SaaS applications
- Dashboards
- Admin panels
- Web3 interfaces
- Portfolio websites
- UI redesign requests
- Premium UI requests

### Load `references/anti-ai-design.md` ONLY when:

- The user requests a premium or polished design
- The user asks to improve or redesign an existing UI
- Generating a complete page or application
- Before finalizing a landing page, dashboard, or marketing website

**Do NOT load `references/anti-ai-design.md` for:**

- Simple components
- Bug fixes
- Small UI edits
- Individual buttons
- Forms
- Tables
- Navigation updates

For narrow, purely mechanical requests (e.g. "what's the install command for the
dialog component"), neither design file is needed.

### Self-review (only when `anti-ai-design.md` is loaded)

Before returning the final result, perform one concise self-review pass against the
design layer, verifying:

- Visual hierarchy
- Typography
- Spacing
- Layout balance
- Color harmony
- Component consistency
- Accessibility
- Mobile responsiveness
- Overall premium quality

**Only revise if a significant issue is detected.** Avoid unnecessary iterations — one
review pass, fix real problems, then finalize.

## Scope & Restraint

The taste layer covers *how it looks*; this layer governs *how much you build*. Default
to the **minimum complete solution** — everything the request needs, and nothing it did
not ask for. Restraint is a quality signal, not a shortcut: a small surface done with
conviction reads as more premium than a sprawling one done at average quality.

### Build only what was asked

- **Scope to the request.** Deliver exactly the pages, sections, and components named
  or clearly implied. When in doubt, build less and let the user ask for more.
- **Never invent surface area.** Do not add navigation items, routes, or pages that were
  not requested. This specifically means **no** invented Docs, Blog, Careers, Changelog,
  Pricing, About/Company, Team, Governance, SDK/API, Integrations, Security/Audits,
  Status, or Ecosystem/Community pages — and no nav links pointing to them — unless the
  user explicitly asks. A single-page request stays a single page.
- **No filler sections.** Prefer a few high-conviction sections over many average ones.
  A landing page with 3 sharp sections beats one with 9 generic ones (hero + features +
  testimonials + logos + stats + FAQ + CTA + newsletter + footer-mega) added on autopilot.
  Each section must earn its place with a distinct job.

### Copy & content discipline

- **Concise marketing copy.** Write tight, specific headlines and subcopy. No padding,
  no throat-clearing, no three-adjective stacks. One clear idea per section.
- **No placeholder content.** Do not ship lorem ipsum, `#` dead links, empty `href=""`,
  fake logos, invented company names/metrics/testimonials, or "Coming soon" stubs. If a
  piece of real content is genuinely unknown, use a small, honest, clearly-marked
  placeholder and call it out to the user rather than fabricating specifics.

### Don't over-engineer the UI

- **Reach for complexity only when the content demands it.** No carousels, mega-menus,
  multi-step wizards, command palettes, animation systems, or state management added
  speculatively. Simpler markup that reads clearly wins over clever machinery.
- **Favor clarity over quantity** at every fork: fewer components, fewer variants, fewer
  dependencies, fewer abstractions — chosen deliberately, not maximally.

> This section is always in force for any generative UI request. It does not require a
> reference file and does not change the loading rules above — it constrains *scope*,
> while the design layer constrains *style*.

## Quick Start

Initialize Shadcn UI in an existing Next.js project:

```bash
npx shadcn@latest init
```

Add components as needed:

```bash
npx shadcn@latest add button card dialog
```

Import and use:

```tsx
import { Button } from "@/components/ui/button"

export default function Page() {
  return <Button variant="outline">Click me</Button>
}
```

> For the full CLI reference (all commands, flags, `components.json` schema), see **`references/cli-and-configuration.md`**.

## Core Workflow

Follow this standard process when building with Shadcn UI:

1. **Initialize** — Run `npx shadcn@latest init` to generate `components.json` and set up paths
2. **Add components** — Run `npx shadcn@latest add [name]` for each component needed
3. **Compose UI** — Combine components in pages and layouts, wrap interactive ones with `"use client"`
4. **Theme** — Configure CSS variables in `globals.css` for light/dark mode
5. **Customize** — Edit component source directly in `components/ui/` when needed

## Component Import Convention

All Shadcn components install to `components/ui/` and use the `@/` path alias:

```tsx
import { Button } from "@/components/ui/button"
import { Card, CardHeader, CardTitle, CardContent } from "@/components/ui/card"
import { Dialog, DialogTrigger, DialogContent } from "@/components/ui/dialog"
```

Every Shadcn component is a **Client Component** internally (uses Radix UI hooks). When using them in Next.js App Router:
- Import them in files that have `"use client"` at the top, OR
- Import them inside a Client Component wrapper

> For the full component catalog (categorized, with install commands, imports, and variants), see **`references/components.md`**.

## Next.js App Router Integration

### Server vs Client Components

Shadcn components use Radix UI primitives (hooks, refs, event handlers), so they require the client runtime. Apply these rules:

| Scenario | Approach |
|----------|----------|
| Page with only Shadcn components | Add `"use client"` to the page file |
| Page mixing data fetching + UI | Keep page as Server Component; extract interactive parts into a Client Component |
| Layout with providers | Add providers in a `"use client"` wrapper component |

### Provider Setup in `layout.tsx`

Place global providers in a dedicated Client Component:

```tsx
// app/providers.tsx
"use client"
import { ThemeProvider } from "next-themes"
import { TooltipProvider } from "@/components/ui/tooltip"

export function Providers({ children }: { children: React.ReactNode }) {
  return (
    <ThemeProvider attribute="class" defaultTheme="system" enableSystem>
      <TooltipProvider>
        {children}
      </TooltipProvider>
    </ThemeProvider>
  )
}
```

```tsx
// app/layout.tsx (Server Component)
import { Providers } from "./providers"

export default function RootLayout({ children }: { children: React.ReactNode }) {
  return (
    <html lang="en" suppressHydrationWarning>
      <body>
        <Providers>{children}</Providers>
      </body>
    </html>
  )
}
```

> For layout patterns, responsive design, and component composition, see **`references/composition-patterns.md`**.

## Form Building

Shadcn forms use **React Hook Form** + **Zod** for validation + Shadcn Form components for UI:

```bash
npx shadcn@latest add form input label
npm install zod
```

Core pattern:

```tsx
"use client"
import { useForm } from "react-hook-form"
import { zodResolver } from "@hookform/resolvers/zod"
import { z } from "zod"
import { Form, FormField, FormItem, FormLabel, FormControl, FormMessage } from "@/components/ui/form"
import { Input } from "@/components/ui/input"
import { Button } from "@/components/ui/button"

const schema = z.object({
  email: z.string().email(),
  name: z.string().min(2),
})

export function MyForm() {
  const form = useForm<z.infer<typeof schema>>({
    resolver: zodResolver(schema),
    defaultValues: { email: "", name: "" },
  })

  function onSubmit(values: z.infer<typeof schema>) {
    // handle submission
  }

  return (
    <Form {...form}>
      <form onSubmit={form.handleSubmit(onSubmit)} className="space-y-4">
        <FormField control={form.control} name="email" render={({ field }) => (
          <FormItem>
            <FormLabel>Email</FormLabel>
            <FormControl><Input placeholder="email@example.com" {...field} /></FormControl>
            <FormMessage />
          </FormItem>
        )} />
        <Button type="submit">Submit</Button>
      </form>
    </Form>
  )
}
```

> For advanced form patterns (select, checkbox, date picker, dynamic arrays, Server Actions), see **`references/forms.md`** and **`examples/form-with-validation.tsx`**.

## Data Tables

Shadcn data tables use **TanStack Table** with a 3-file architecture:

```bash
npx shadcn@latest add table
npm install @tanstack/react-table
```

| File | Purpose |
|------|---------|
| `columns.tsx` | Define `ColumnDef[]` with accessors, headers, cell renderers |
| `data-table.tsx` | Reusable `<DataTable>` component with `useReactTable` |
| `page.tsx` | Fetch data (Server Component) and pass to `<DataTable>` |

> For column definitions, sorting, filtering, pagination, and row selection patterns, see **`references/data-tables.md`** and **`examples/data-table-example.tsx`**.

## Theming

Shadcn UI uses **CSS variables** in `globals.css` for all color tokens. Modern Shadcn uses the `oklch` color format:

```css
:root {
  --background: oklch(1 0 0);
  --foreground: oklch(0.145 0 0);
  --primary: oklch(0.205 0 0);
  --primary-foreground: oklch(0.985 0 0);
  /* ... */
}

.dark {
  --background: oklch(0.145 0 0);
  --foreground: oklch(0.985 0 0);
  /* ... */
}
```

Enable dark mode with `next-themes`:

```bash
npm install next-themes
```

> For the complete variable list, dark mode toggle component, TweakCN editor workflow, sidebar tokens, and custom colors, see **`references/theming-and-dark-mode.md`**.

## Charts

Shadcn Charts wrap **Recharts** with themed components:

```bash
npx shadcn@latest add chart
npm install recharts
```

Core pattern: define a `ChartConfig` object mapping data keys to labels and colors, wrap Recharts components in `<ChartContainer>`:

```tsx
const chartConfig = {
  desktop: { label: "Desktop", color: "var(--chart-1)" },
  mobile: { label: "Mobile", color: "var(--chart-2)" },
} satisfies ChartConfig
```

> For all chart types, tooltip/legend configuration, and responsive patterns, see **`references/charts.md`** and **`examples/chart-config-example.tsx`**.

## Blocks

Blocks are pre-built, full-page or section-level compositions (dashboards, login pages, sidebars). Copy the block source into the project and install required components.

> For the block catalog, file structures, dependencies, and the sidebar system, see **`references/blocks.md`** and **`examples/dashboard-layout.tsx`**.

## Key Rules

| Do | Don't |
|----|-------|
| Use `npx shadcn@latest add` to install components | Install components via npm |
| Import from `@/components/ui/...` | Import from `shadcn` or `@shadcn/ui` |
| Use CSS variables for theming (`oklch`) | Hardcode color values in components |
| Add `"use client"` when using interactive components | Use Shadcn components in Server Components without a client wrapper |
| Edit component source in `components/ui/` to customize | Create wrapper components for simple style changes |
| Install all dependencies for blocks | Copy block code without its required components |
| Build the minimum complete solution | Add pages, routes, or nav items nobody requested |
| Ship a few high-conviction sections | Pad the page with filler sections on autopilot |
| Use real, concise copy | Ship lorem ipsum, dead `#` links, or fabricated metrics |
| Keep the UI as simple as the content allows | Add carousels, mega-menus, or wizards speculatively |

> Scope discipline is defined in **Scope & Restraint** above; these rows are its
> enforcement summary.

## Reference Files

### Detailed Guides
- **`references/design-direction.md`** — Visual philosophy: hierarchy, typography, spacing, color, motion, anti-patterns, and the final design checklist (load for any web design / UI request)
- **`references/anti-ai-design.md`** — Diagnostic catalog of AI-generated tells + self-review checklist (load only for premium/redesign/full-page work; see loading rules above)
- **`references/cli-and-configuration.md`** — CLI commands, `components.json` schema, aliases, package managers
- **`references/components.md`** — Full component catalog categorized by type with variants and imports
- **`references/composition-patterns.md`** — Layout patterns, Server/Client components, providers, responsive design
- **`references/forms.md`** — React Hook Form + Zod + Shadcn Form component patterns
- **`references/data-tables.md`** — TanStack Table integration, columns, sorting, filtering, pagination
- **`references/charts.md`** — Recharts integration, ChartConfig, all chart types, tooltips
- **`references/blocks.md`** — Block catalog, sidebar system, dashboard patterns, dependencies
- **`references/theming-and-dark-mode.md`** — CSS variables, oklch, next-themes, TweakCN, custom colors
- **`references/accessibility.md`** — Built-in Radix a11y, developer responsibilities, ARIA patterns

### Code Examples
- **`examples/form-with-validation.tsx`** — Complete form with Zod schema, multiple field types, submit handler
- **`examples/data-table-example.tsx`** — Data table with columns, sorting, and pagination
- **`examples/dashboard-layout.tsx`** — Dashboard layout with sidebar, header, and content area
- **`examples/chart-config-example.tsx`** — Bar chart with full ChartConfig, tooltip, and legend

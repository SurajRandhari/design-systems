# DESIGN-SYSTEM-RULES (machine-readable; read first)

Scope: every Next.js (App Router) project I build. Values change per project; this contract does not.
Non-negotiable: every page and component is designed AND validated on mobile, tablet, desktop and large desktop, with excellent Core Web Vitals, minimal JS, no layout shift, no render delay.

## 1. Stack
- Next.js App Router, React Server Components by default.
- Tailwind CSS. shadcn/ui primitives in `components/ui/`.

## 2. Tokens (see 01-design-tokens/)
- Three layers: Primitive values -> Semantic tokens -> Components. Components consume only semantic tokens.
- Token NAMES are the contract; VALUES are per project.
- Forbidden in components: raw palette names (`blue-500`, `gray-900`), hex/rgb, arbitrary px values (`mt-[37px]`), arbitrary shadows, inline style colors.
- Color utilities: `bg-primary text-primary border-primary` (+ `-hover -active -disabled -foreground`), `secondary`, `tertiary`, `bg-background(-secondary|-tertiary)`, `text-foreground(-secondary|-muted|-inverse)`, `text-heading`, `border-border(-secondary|-strong)`, `success warning error info`.
- Type utilities: `text-display text-h1..h6 text-body-lg text-body text-body-sm text-label text-caption text-button` (rem + clamp()).
- Also: `shadow-xs..xl`, `rounded-sm..2xl,full` (token `radius-*`), `duration-fast|normal|slow`, `ease-standard|in|out|in-out`, `z-base|dropdown|sticky|header|overlay|modal|toast`, `space-*`.

## 3. Responsive (see 04-responsive/)
- Mobile-first: base = mobile; enhance up through tablet, desktop, large desktop. Never desktop-first.
- Validate at 320, 375, 390, 414, 768, 1024, 1280, 1440, 1920. No horizontal scroll.

## 4. Structure (see 02-architecture/)
```
app/  components/{ui,layout,common,<page>,admin}/  lib/{api,data,constants,config,utils}/  hooks/  types/  public/
```
- Page-specific -> `components/<page>/` · shared -> `components/common/<Group>/` · layout -> `components/layout/` · shadcn -> `components/ui/`.
- Admin panels use the SAME architecture (`app/admin/**`, `components/admin/`). No separate architecture.
- No barrel `index.js` files. Direct imports only.
- Data flow: DB/API -> `lib/api` -> Server Component -> Page -> Section -> Reusable Component -> UI primitive.
- Presentation components never fetch or touch the DB.

## 5. Server/Client
- Server Component by default. `"use client"` only for state, effects, refs, browser APIs, event-driven UI, client-only libs.
- Preferred: Server Page -> Server Section -> small Client Island. Never a whole page client-side without need.

## 6. Quality gates
- Accessibility (WCAG 2.2 AA): semantic HTML, keyboard, visible focus, labels, headings, contrast, alt, reduced motion, 44px targets.
- Core Web Vitals targets: LCP <= 2.5s, INP <= 200ms, CLS <= 0.1; also monitor FCP, TBT, TTFB, Speed Index. These are targets and budgets, not guarantees; measured results depend on hosting, backend, content, assets, traffic and third parties.
- Measure before optimizing; re-measure after. No claim without a number.
- `priority` only on the likely-LCP image. All media sized. `next/image`, `next/font`.
- No unnecessary dependencies, third-party scripts, wrappers, hooks, providers, abstractions.

## 7. Audit and debug (see 06-audit/)
- Audit every project: UI, Responsive, Accessibility, Performance, Core Web Vitals, SEO, Architecture, Code Quality.
- Debug: Reproduce -> route -> component -> layer -> baseline -> root cause -> smallest fix -> re-measure -> regression check.

## 8. Safety
- No public URL change without approval. No accidental `noindex`.
- Don't delete working code, rename routes, replace APIs, or change DB/business logic unasked. Document conflicts before changing.
- Don't commit or push unless told.

## 9. Fixed vs variable
Variable per project: brand colors, fonts, weights, exact type scale, shadow strength, radius values, content, component variants.
Fixed: token names/categories, folder and component architecture, data architecture, naming, responsive method, accessibility and performance standards, audit method, AI rules.

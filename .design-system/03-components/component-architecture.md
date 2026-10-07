# Component architecture contract

Every project uses this component structure:

```
components/
├── ui/        shadcn primitives
├── layout/    Container, Section, Header, Footer, PageWrapper
├── common/    shared reusable components
├── home/      page-specific
├── about/
├── pricing/
├── admin/
└── ...
```

## Composition chain

```
shadcn primitive            components/ui/
        ↓
common reusable component   components/common/<Group>/
        ↓
page-specific component     components/<page>/  (Section-level)
        ↓
Page                        app/**/page.js
```

- **Primitive** (`ui/`): unstyled-by-brand building block (Button, Dialog, Input). No business meaning.
- **Common** (`common/`): reusable, brand-aware composition built from primitives (PrimaryButton, ProductCard, ContactForm, MobileNav). No page knowledge, no data fetching.
- **Page-specific** (`<page>/`): sections and pieces used by one page (`HeroSection`, `PricingTableSection`). Receive data via props from the page.
- **Layout** (`layout/`): page chrome and structural wrappers.

## Promotion rule

Start page-specific. When a second page needs it, move it to `common/<Group>/` (update imports; don't duplicate).

## Rules

- One component per file; PascalCase; direct imports; **no barrel files**.
- Server Component by default; client islands at the leaves (`../02-architecture/server-client.md`).
- Props small and explicit; compose with `children`/slots instead of boolean-prop explosions; variants only when 2+ exist.
- No data access in components; no hidden global state.
- No wrapper that merely renames another component. A wrapper must add real defaults, variants or behavior.
- No hooks, context providers or state libraries without a concrete stated need.
- Reusable components accept and forward `className` and rest props (including `aria-*`).

## Component quality checklist

Before a component is "done" it is verified for:
Desktop ✓ Tablet ✓ Mobile ✓ Keyboard ✓ Accessibility ✓ Loading state ✓ Empty state ✓ Error state (where relevant) ✓ Hover ✓ Focus ✓ Disabled ✓ Responsive typography ✓ Responsive spacing ✓ Image optimization ✓ Performance ✓

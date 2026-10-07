# shadcn/ui contract

This repository only documents the convention. It installs nothing and contains no shadcn components.

shadcn components are **UI primitives**. They live in `components/ui/` (shadcn's standard location, kept in every project).

```
shadcn primitive            components/ui/
        ↓
common reusable component   components/common/<Group>/
        ↓
page-specific component     components/<page>/
```

```
components/
  ui/       button, dialog, input, dropdown-menu, table ...   (shadcn)
  common/   Buttons/PrimaryButton, Forms/ContactForm ...      (built from ui/)
  home/     HeroSection ...                                   (uses common/ and ui/)
```

## Compatibility rules

- Project tokens keep shadcn's expected semantic variable names where they overlap (`background`, `foreground`, `primary`, `primary-foreground`, `secondary`, `muted`, `accent`, `destructive`, `border`, `input`, `ring`, `card`, `popover`, `radius`) so `shadcn add` output inherits the brand. Contract tokens are a superset; each project maps overlaps (e.g. `destructive` -> `error`, `muted` -> `background-secondary`).
- If the project disables the default Tailwind palette, shadcn components that use raw colors must be adjusted to semantic tokens when added.
- The shadcn `utils` alias must resolve to wherever the project keeps its class-merge helper (typically `lib/utils/`).
- Animation helper plugins required by shadcn components are a project-level dependency decision.

## Rules

- Add components via the CLI, then review: tokens only, accessibility intact, no avoidable `"use client"`.
- Prefer wrapping (`common/`) or adding a variant over editing shadcn source heavily (keeps upgrades easy).
- No business logic, data fetching or page-specific code in `ui/`. `lib/` never imports from `ui/`.
- Add only the primitives actually used; each can add client JS.
- Verify mobile behavior: Dialog -> bottom sheet/full screen on mobile; Select/Dropdown targets >= 44px; Table -> scroll wrapper or stacked layout.
- Tailwind v3 vs v4 differences are handled in the project's config; the contract (names) is identical.

# Component rules

1. **Semantic tokens only.** Colors, type, spacing, radius, shadow, motion, z-index come from tokens. No raw hex or arbitrary px values.
2. **Server by default.** `"use client"` only for real interactivity, at the leaf.
3. **Semantic HTML first.** `<button>` for actions, `<a>`/`next/link` for navigation, `<nav> <main> <section aria-labelledby> <ul>`, one `<h1>`, no skipped heading levels.
4. **Mobile-first classes.** Base = mobile; add `sm: md: lg: xl: 2xl:`.
5. **No duplicated class strings.** Repeated 3+ times -> component, variant, or custom utility. Don't create a component just to rename a class.
6. **States.** Every interactive component defines hover, `focus-visible`, active, disabled, and (where relevant) loading, empty, error.
7. **Reserve space.** Images get dimensions or aspect ratio; async areas get skeletons sized like the final content.
8. **No data access** in presentation components (`../02-architecture/data-flow.md`).
9. **Merge classes** with the project's class-merge helper so `className` overrides work.
10. **Forward `className` and rest props** on reusable components; never swallow `aria-*`.

## Common component conventions

- **Buttons** (`components/common/Buttons/`): wrap the shadcn Button only to bake in the project's variant/size defaults (e.g. `PrimaryButton`, `SecondaryButton`, `OutlineButton`). Navigation buttons render as links. Touch target >= 44px; labels wrap without clipping.
- **Cards**: media (fixed aspect) -> title (heading level via prop) -> text -> action. Whole-card links: one link on the title extended to the card, never nested links.
- **Forms**: visible `<label>` per field, `aria-describedby` for help/error, `aria-invalid`, correct `type`/`inputmode`/`autocomplete`; errors announced (live region); submit disabled only while pending.
- **Modals**: shadcn Dialog (focus trap, Esc, focus return); full-screen/bottom sheet on mobile, centered on tablet and up.
- **Navigation**: see `../04-responsive/component-responsive-patterns.md`; the mobile menu toggle is the only client island in the header.

## Definition of done

Desktop ✓ Tablet ✓ Mobile ✓ Keyboard ✓ Accessibility ✓ Loading ✓ Empty ✓ Error ✓ Hover ✓ Focus ✓ Disabled ✓ Responsive type ✓ Responsive spacing ✓ Image optimization ✓ Performance ✓

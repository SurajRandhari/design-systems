# Responsive design contract

Every project ALWAYS supports **Mobile, Tablet, Desktop, Large Desktop**. Responsive design is mandatory, not a polish step.

```
Mobile-first
     ↓
Tablet enhancement
     ↓
Desktop enhancement
     ↓
Large desktop enhancement
```

Never: design desktop, then shrink until mobile works.

## Validation widths

`320 · 375 · 390 · 414 · 768 · 1024 · 1280 · 1440 · 1920` (add `640` where tablet logic exists). Also test landscape phones and 200% zoom.

## Method

1. Design the 320-414 layout first: single column, stacked, thumb-reachable actions, readable type.
2. Add enhancements at the width where content needs them (not at a device name).
3. Prefer intrinsic and fluid layout (`auto-fit/minmax` grids, `flex-wrap`, `clamp()` tokens, container queries) over many breakpoints.
4. Cap content width on large screens (`container-page`); extra room becomes whitespace, not stretched content.
5. Each component declares its mobile / tablet / desktop / large-desktop behavior (`component-responsive-patterns.md`).

## Tiers

| Tier | Behavior |
|---|---|
| Mobile | Single column; stacked sections; mobile navigation; full-width primary actions; 44px targets; minimal sticky UI |
| Tablet | Balanced split/2-column; condensed navigation; inline actions |
| Desktop | Multi-column; full navigation; hover affordances (with touch equivalents); 3-4 column grids when content allows |
| Large desktop | Container capped; larger media/spacing tokens; no stretched text lines |

## Hard rules

- No horizontal page scroll at any width.
- No fixed pixel widths for containers (`w-full max-w-*`).
- Flex/grid children holding text get `min-w-0`; long strings wrap.
- Use fluid tokens (`clamp`) for type and spacing; avoid unnecessary breakpoints.
- Don't assume `grid-cols-3` is enough: check content length, image ratios, button wrapping, heading wrapping, spacing, touch targets and vertical rhythm, plus 1-item and long-title cases.
- Safe areas and dynamic viewport units for fixed/full-height elements.
- Hover-only information must have a touch/keyboard equivalent.

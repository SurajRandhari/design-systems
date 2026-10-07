# Spacing contract

Two parts: a base scale and semantic layout tokens.

## Base scale: `space-*`
A consistent rem-based scale (e.g. multiples of 0.25rem). Used for component internals (padding, gaps within a component). Utilities: `p-*`, `m-*`, `gap-*`, `space-y-*` from the framework's scale.

## Semantic spacing tokens (names are the contract)

| Token | Purpose | Responsive behavior |
|---|---|---|
| `space-gutter` | Container side padding | Fluid (small on mobile, larger on desktop) |
| `space-section` | Vertical padding between page sections | Fluid |
| `space-gap` | Gap between grid/card siblings | Fluid |
| `space-stack` | Vertical rhythm inside a content block (heading -> text -> CTA) | Fluid |
| `space-component-sm` `-md` `-lg` | Internal padding of cards, panels, controls | Fixed per size, rem |
| `touch-target` | Minimum interactive size (>= 2.75rem = 44px) | Fixed |

Fluid tokens use `clamp()` in rem; values are project-specific. Example shape: `--space-section: clamp(3rem, 2rem + 5vw, 7rem);`

## Rules

- No arbitrary spacing (`mt-[37px]`). If a value repeats 3+ times, tokenize it.
- Prefer `gap` and parent-owned spacing over per-child margins.
- rem-based so spacing scales with user font size.
- Interactive controls >= 44x44px; >= 8px between adjacent targets.
- Reserve space for async content (min-height / aspect-ratio) to prevent layout shift.
- Consistent vertical rhythm: sections use `space-section`, blocks use `space-stack`, grids use `space-gap`.

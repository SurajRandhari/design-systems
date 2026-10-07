# Shadow contract

Tokens: `shadow-xs` `shadow-sm` `shadow-md` `shadow-lg` `shadow-xl`. Values (strength, color, layering) are project-specific.

| Token | Typical use |
|---|---|
| `shadow-xs` | Inputs, subtle separation |
| `shadow-sm` | Cards at rest |
| `shadow-md` | Raised cards, dropdowns |
| `shadow-lg` | Popovers, sticky header on scroll |
| `shadow-xl` | Modals, dialogs |

## Rules

- No arbitrary shadows (`shadow-[0_4px_...]`); use a token.
- Elevation expresses hierarchy; don't mix more than two levels in one view.
- On large or frequently repainted surfaces, avoid animating `box-shadow`; fade a pseudo-element's `opacity` instead.
- In dark mode, prefer borders over heavy shadows.

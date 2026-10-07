# Z-index contract

One semantic ladder. Names are fixed; numbers are project-defined but must preserve this order (low to high).

| Token | Layer |
|---|---|
| `z-base` | Normal flow (0) |
| `z-dropdown` | Dropdowns, popovers, tooltips anchored to content |
| `z-sticky` | Sticky sub-navs, table headers, TOC |
| `z-header` | Site header / app bar |
| `z-overlay` | Backdrops, scrims, mobile nav panel |
| `z-modal` | Dialogs, sheets |
| `z-toast` | Toasts, skip-link on focus, topmost notices |

## Rules

- No magic numbers (`z-[9999]`). Use a token; if a new layer is genuinely needed, add a token in its correct position.
- Don't fight stacking contexts with larger numbers; fix the context (`isolation`, parent `position`).
- Limit simultaneous sticky layers on mobile (they eat viewport height).

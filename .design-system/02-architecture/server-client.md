# Server / Client component contract

Default: **Server Component**.

Use a Client Component (`"use client"`) only when the component needs:
- state (`useState`, `useReducer`)
- effects or refs (`useEffect`, `useRef`)
- browser APIs (`window`, `localStorage`, `IntersectionObserver`)
- event handlers that drive client state
- interactive UI (menus, tabs, carousels, dialogs beyond CSS)
- client-only libraries

## Preferred shape

```
Server Page
    ↓
Server Section
    ↓
Small Client Island
```

Not: `Client Page -> everything client-side`.

## Rules

- Push `"use client"` to the leaf: only the interactive part (e.g. the menu toggle), not the whole header.
- Server Components may pass server-rendered children into client components (children slot) so content stays server-rendered.
- Props crossing the boundary must be serializable.
- Never add `"use client"` "just in case" or to silence an error without understanding it.
- Prefer CSS/HTML for disclosure, hover, sticky, scroll-snap, `<details>`, native form behavior before reaching for client JS.
- Heavy client widgets (charts, maps, editors) load with dynamic import, on visibility or interaction.
- Keep client islands small; track their count and size (`../05-performance/budgets.md`).
- Quick test: *does this need to run in the browser?* No -> Server.

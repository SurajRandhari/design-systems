# JavaScript performance

Less JS = better INP, TBT, FCP and LCP.

## Rules

- Server Components by default; small leaf Client Components only. Track the number and size of `"use client"` files.
- Don't make pages or layouts client components. Keep client-only libraries in leaves.
- Dependencies: none added without a stated reason and a size check. Remove unused ones only after confirming usage.
- Prefer CSS: transitions/keyframes, scroll-snap, `position: sticky`, `<details>`, `:has()`, container queries, native `popover`.
- Animation libraries only if CSS can't do it; dynamic-import and scope them.
- Heavy widgets (charts, maps, editors, 3D, carousels): dynamic import, client-only, load on visibility/interaction.
- `useEffect`: justify each one. Not for derived state, data the server can deliver, or what events can do.
- Avoid global listeners (scroll/resize); prefer `IntersectionObserver`/`ResizeObserver`/CSS; passive listeners; always clean up.
- Avoid unnecessary re-renders: keep state local, split components, memoize only after profiling.
- Break up long tasks; use transitions for non-urgent updates; workers for heavy compute.
- Import specific symbols (icons/utilities); no whole-library imports.
- Keep browser targets modern; no unnecessary polyfills.

## Debug tools
Bundle analyzer · DevTools Performance (long tasks) · Coverage (unused JS) · React Profiler · framework build route table (first-load JS).

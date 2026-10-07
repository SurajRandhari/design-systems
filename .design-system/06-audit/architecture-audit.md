# Architecture audit

For existing projects, run this first and **record conflicts before changing anything**.

### Folder and file placement
- **Expected:** page components in `components/<page>/`, shared in `components/common/<Group>/`, layout in `components/layout/`, shadcn only in `components/ui/`, admin in `components/admin/`, logic in `lib/`.
- **Common problems:** business components in `ui/`, logic in `components/lib/`, one giant `components/` root, per-page duplicates, separate admin architecture.
- **How to debug:** list `components/` two levels deep; trace imports crossing layers.
- **How to fix:** move to the narrowest correct scope (document first, preserve behavior); promote to `common/` when used by 2+ pages.

### Barrel files
- **Expected:** none.
- **How to debug:** search for `index.js`/`index.jsx` in `components`, `app`, `lib`.
- **How to fix:** replace with direct imports; delete the barrel after updating all importers.

### Server / client boundary
- **Expected:** server by default; `"use client"` only on leaf interactive components.
- **Common problems:** client pages/layouts, `"use client"` "just in case", providers wrapping the whole app, `useEffect` data fetching.
- **How to debug:** list files containing `"use client"`; justify each (state/effect/ref/browser API/handlers).
- **How to fix:** extract the interactive part into a small child; fetch on the server; pass props.

### Data flow
- **Expected:** DB/API -> `lib/api` -> server page -> section -> component -> primitive.
- **Common problems:** fetch/ORM/DB calls inside components, secrets reachable from client, request waterfalls.
- **How to debug:** search components for `fetch(`, DB client calls, `process.env`.
- **How to fix:** extract to `lib/api/*` (server-only), fetch in the page (in parallel), pass props.

### Dependencies and abstraction
- **Expected:** no unused or duplicate dependencies; no needless wrappers/hooks/providers.
- **How to debug:** dependency-usage tooling; bundle analyzer; review `package.json`.
- **How to fix:** remove after verifying usage; inline trivial wrappers.

### Config conflicts
- **Expected:** tokens defined in one place with contract names; shadcn aliases match folders; framework config minimal and documented.
- **How to debug:** inspect `package.json`, framework config, Tailwind setup, global CSS, shadcn config.
- **How to fix:** document conflicts, migrate token by token, keep public URLs.

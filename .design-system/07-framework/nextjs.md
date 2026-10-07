# Next.js conventions

Conventions only; no implementation lives in this repository.

- **App Router** for all projects; Server Components by default (`../02-architecture/server-client.md`).
- **Rendering:** static/ISR for public content; dynamic only for per-user/real-time data. Dynamic APIs (`cookies`, `headers`, `searchParams`) opt a route into dynamic rendering; use deliberately.
- **Images:** `next/image` always for content images; `sizes` required; `priority` only on the likely-LCP image; configure modern formats and the device-size list the design actually uses; restrict remote hosts explicitly.
- **Fonts:** `next/font` (self-hosted); one family, only used weights, `display: swap`; expose as a CSS variable consumed by the typography tokens.
- **Scripts:** `next/script` with `lazyOnload`/`afterInteractive`; never global unless every page needs them.
- **Links/navigation:** `next/link`; semantic anchors; preserve public URLs.
- **Metadata:** `metadata`/`generateMetadata` per page (title, description, canonical, robots, Open Graph, Twitter); `metadataBase` set once in the root layout; sitemap and robots via the route-file conventions.
- **Viewport:** device-width, initial-scale 1; never disable user zoom.
- **Streaming:** `loading.js` + `Suspense` with size-reserving skeletons.
- **Errors:** `error.js`, `not-found.js` per segment as needed.
- **Config:** keep `next.config` minimal; add options only for a measured need. Document each non-default option.
- **Env:** secrets server-side only; `NEXT_PUBLIC_*` is public by definition.
- **Bundle:** import specific symbols (icons, utilities); consider package-import optimization only after measuring.
- **Never:** change public URLs without approval; make whole pages client components; introduce `noindex` on public pages accidentally.
